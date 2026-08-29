---
category: general
date: 2026-08-08
description: Aspose.Cells'ta pivot tabloyu kopyalama ve Java kullanarak aralığı çalışma
  kitabına kopyalama. CopyOptions ile bir pivot tabloyu çoğaltmanın tam adımlarını
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: tr
lastmod: 2026-08-08
og_description: Aspose.Cells'te pivot tabloyu nasıl kopyalar ve Java ile aralığı çalışma
  kitabına nasıl kopyalarsınız. Pivot tabloyu CopyOptions kullanarak çoğaltmak için
  bu kapsamlı rehberi izleyin.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Aspose.Cells'ta pivot nasıl kopyalanır – aralığı çalışma kitabına kopyala
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Aspose.Cells'ta pivot tablo nasıl kopyalanır – aralığı çalışma kitabına kopyala
url: /tr/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells’ta pivot kopyalama – aralığı çalışma kitabına kopyalama

Bir Excel dosyasında **pivot nasıl kopyalanır** gerektiğinde, bu kılavuz tam süreci gösterir. Eğitim sonunda **aralığı çalışma kitabına kopyalama** işlemini pivot tablo tanımını koruyarak yapabileceksiniz.

Örnek Java kullanılarak verilmiştir, ancak aynı kavramlar Aspose.Cells ile çalışan herhangi bir .NET dili için de geçerlidir. Harici bir araç gerekmez—sadece Aspose.Cells for Java kütüphanesi ve temel bir geliştirme ortamı yeterlidir.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java Development Kit (JDK) 8 veya üzeri.
* Bağımlılıkları yönetmek için Maven veya Gradle (örnek Maven kullanır).
* Projenize eklenmiş Aspose.Cells for Java 23.9 (veya en yeni sürüm).
* İlk çalışma sayfasında en az bir pivot tablo içeren bir giriş çalışma kitabı (`input.xlsx`).

Bu öğeler hazır olduğunda, kod çalışma kitabına eriştiğinde çalışma zamanı hataları önlenir.

## Aspose.Cells ile pivot nasıl kopyalanır

Bu bölüm, `CopyOptions` sınıfını kullanarak bir sayfanın bir bölümünden diğerine **pivot nasıl kopyalanır** sorusunun adım adım yanıtını verir.

### Adım 1: Aspose.Cells’ı projenize ekleyin

Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Bu adımın önemi*: Kütüphane, **aspose.cells copy range** işlemleri için gerekli `Workbook`, `CopyOptions` ve diğer sınıfları sağlar. Bağımlılık olmadan derleyici bu tipleri çözemeyecektir.

### Adım 2: Kaynak çalışma kitabını yükleyin

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Dosyanın yüklenmesi, elektronik tabloyun bellek içi bir temsilini oluşturur. `Workbook` nesnesi, çalışma sayfalarına, hücrelere ve pivot tablolara erişim sağlar.

### Adım 3: Pivot tabloyu dahil etmek için kopyalama seçeneklerini yapılandırın

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` Aspose.Cells’a işlemin pivot tablo meta verilerini koruması gerektiğini söyler. Bu bayrak bırakılırsa, pivot tablo statik verilere dönüşür ve etkileşimini kaybeder.

### Adım 4: Pivot tabloyu içeren istenen aralığı kopyalayın

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange` yöntemi hücreleri, biçimlendirmeyi ve önceki adımda ayarlanan seçenekler sayesinde aralığa kesişen pivot tabloları da kopyalar. Bu, **copy range to workbook** işlevinin çekirdeğidir.

### Adım 5: Değiştirilen çalışma kitabını kaydedin

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Kaydetme, değişiklikleri yeni bir dosyaya (`output.xlsx`) yazar. Artık bu dosyayı Excel’de açıp, pivot tablonun tam olarak kopyalandığını görebilirsiniz.

## Tam, çalıştırılabilir örnek

Tüm parçaları birleştirerek, derleyip çalıştırabileceğiniz tam program aşağıdadır:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Beklenen sonuç

* `output.xlsx` aynı verileri `input.xlsx` ile içerir.
* Kaynak aralığı dolduran pivot tablo, hedef hücrelerde aynı şekilde (filtreler, yenileme yeteneği vb.) bulunur.
* `copyRange` tüm hücre bloğunu kopyaladığından, hücre biçimlendirmeleri, formüller ve sütun genişlikleri korunur.

## Yaygın sorular ve kenar durumları

**Hedef aralık mevcut bir pivot tabloyla çakışırsa ne olur?**  
Aspose.Cells hedef hücreleri üzerine yazar. Veri kaybını önlemek için hedef alanın boş olduğundan emin olun veya mevcut pivot tabloyu önce taşıyın.

**Pivot tabloyu farklı çalışma sayfalarına kopyalayabilir miyim?**  
Evet. `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` ifadesinde `targetSheetIndex` hedef sayfayı gösterir.

**`setCopyPivotTable(true)` veri kaynağını da kopyalar mı?**  
Yöntem yalnızca pivot önbellek referansını kopyalar. Kaynak veri aynı çalışma kitabındaysa, hedef pivot aynı önbelleğe işaret eder. Önbelleği çoğaltmak için yeni bir pivot önbelleği manuel olarak oluşturmanız gerekir.

**Büyük bir aralığı verimli şekilde nasıl kopyalarım?**  
Çok büyük aralıkları kopyalarken, yalnızca gerektiğinde `CopyOptions.setCopyFormula(true)` ve `setCopyDataValidation(true)` kullanın. Seçenek sayısını azaltmak performansı artırabilir.

## Güvenilir **aspose.cells copy range** kullanımı için ipuçları

* **Pro ipucu:** Aralık formüller içeriyorsa ve pivot önbelleğe bağımlıysa, kopyalama sonrası her zaman `workbook.calculateFormula()` çağırın.
* **Dikkat:** Gizli çalışma sayfaları. `copyRange` yalnızca görünür çalışma sayfalarında çalışır; gizli sayfayı indeksle açıkça belirtmezseniz işlem gerçekleşmez.
* **Sürüm kontrolü:** `setCopyPivotTable` bayrağı Aspose.Cells 20.9’dan itibaren mevcuttur. Kütüphane sürümünüzün bu özelliği desteklediğinden emin olun.

## Sonuç

Artık Aspose.Cells’ta **pivot nasıl kopyalanır** ve **aralığı çalışma kitabına kopyalama** işlemini pivot işlevselliğini tamamen koruyarak yapabilirsiniz. Kütüphaneyi ekleme, çalışma kitabını yükleme, `CopyOptions` yapılandırma, kopyalama ve kaydetme adımları, diğer kopyala‑yapıştır senaryolarına da uyarlanabilecek tekrarlanabilir bir desen oluşturur.

Sonraki adımda, **aspose.cells copy range** konusundaki grafik, koşullu biçimlendirme ve veri doğrulama gibi ek özellikleri keşfedin. Farklı dosya formatları arasında (XLSX → XLS) kopyalama deneyerek otomasyon yeteneklerinizi genişletin. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve API özelliklerini daha iyi kavramanızı ve projelerinizde alternatif uygulama yaklaşımları denemenizi sağlar.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}