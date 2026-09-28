---
category: general
date: 2026-09-11
description: Aspose.Cells kullanarak yeni bir çalışma sayfası oluşturun ve Excel aralığını
  kopyalayın. Pivot tablolarını koruyarak aralığı sayfalar arasında nasıl kopyalayacağınızı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: tr
lastmod: 2026-09-11
og_description: Aspose.Cells ile yeni bir çalışma sayfası oluşturun ve Excel aralığını
  kopyalayın. Bu öğretici, aralığı sayfalar arasında kopyalama ve özet tabloları bozulmadan
  koruma adımlarını gösterir.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Yeni çalışma sayfası oluştur ve Excel aralığını kopyala – Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Yeni bir çalışma sayfası oluşturun ve Aspose.Cells ile Excel aralığını kopyalayın
url: /tr/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yeni çalışma sayfası oluşturma ve Aspose.Cells ile Excel aralığını kopyalama

Bir Excel dosyasında **create new worksheet** ve verileri taşımak istiyorsanız, Aspose.Cells bunu basit hale getirir. Bu kılavuz, bir aralıktaki pivot tabloları koruyarak bir sayfadan diğerine Excel aralığını nasıl kopyalayacağınızı tam olarak gösterir.

Nasıl **copy excel range** yapılacağını, **copy range between sheets** nasıl yapılacağını ve Aspose.Cells `copy` metodunun pivot tablo tanımlarını neden koruduğunu öğreneceksiniz. Harici araçlara gerek yok—sadece Aspose.Cells kütüphanesini içeren bir Java projesi.

## Önkoşullar

- Java 17 veya daha yeni bir sürüm yüklü
- Aspose.Cells for Java (version 23.12 veya daha yeni) projenizin classpath'ine eklenmiş
- Kopyalamak istediğiniz aralıkta pivot tablo içeren bir kaynak çalışma kitabı (`input.xlsx`)
- Java sözdizimi ve Maven/Gradle bağımlılık yönetimi konusunda temel bilgi

## Adım 1: Projeyi kurun ve Aspose.Cells'i içe aktarın

Basit bir Maven projesi (veya tercih ederseniz Gradle) oluşturun ve Aspose.Cells bağımlılığını ekleyin:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Ardından Java kaynak dosyanıza gerekli sınıfları içe aktarın:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Bu adımın önemi*: Doğru sınıfları içe aktarmak, `Workbook`, `Worksheet`, `Range` ve aralık transferini gerçekleştirecek `copy` metoduna erişmenizi sağlar.

## Adım 2: Kaynak çalışma kitabını yükleyin

Kopyalamak istediğiniz verileri içeren çalışma kitabını açın. Aşağıdaki kod, belirttiğiniz bir dizinden `input.xlsx` dosyasını yükler:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Açıklama*: `Workbook`, tüm Excel dosyasını temsil eder. Bir kez yüklemek, her sayfa ve hücre koleksiyonuna okuma/yazma erişimi sağlar.

## Adım 3: Pivot tabloyu içeren kaynak aralığı belirleyin

Pivot tabloyu içeren çalışma sayfasını seçin ve kopyalamak istediğiniz tam hücre bloğunu tanımlayın. Bu örnekte A1’den D20’ye kadar olan hücreleri kopyalıyoruz:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Neden önemli*: Bir `Range` nesnesi oluşturarak, Aspose.Cells'e hangi hücrelerin (pivot tablolar gibi gömülü nesneler dahil) çoğaltılması gerektiğini tam olarak bildirirsiniz.

## Adım 4: **Create new worksheet** alacak yeni çalışma sayfasını oluşturun

Şimdi aynı çalışma kitabına yeni bir sayfa ekliyoruz. İşte ana anahtar kelimenin göründüğü nokta:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Açıklama*: Yeni bir sayfa eklemek, kopyalanan verileri izole eder ve **copy excel range** işleminin başarılı olduğunu, orijinal sayfayı etkilemeden doğrulamayı kolaylaştırır.

## Adım 5: Aralığı kopyala – pivot tablo otomatik olarak korunur

`copy` metodunu kullanarak aralığı kaynak sayfadan hedef sayfaya taşıyın. Aspose.Cells formülleri, biçimlendirmeyi ve pivot‑tablo tanımlarını kopyalar:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Neden çalışır*: `copy` metodu, kaynak hücrelerin derin bir kopyasını oluşturur. Sadece değerleri kopyalamaz; pivot önbelleği dahil tüm hücre yapısını yeniden oluşturur. Bu yüzden **copy range aspose.cells** yapabilir ve yeni sayfada işlevsel bir pivot tablo görebilirsiniz.

## Adım 6: Yeni çalışma sayfası ile çalışma kitabını kaydedin

Son olarak, değiştirilmiş çalışma kitabını diske yazın:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Sonuç*: `output.xlsx` artık orijinal sayfayı ve **Copy** adlı yeni bir sayfayı içerir; bu sayfa aynı aralığı, pivot tabloyu da içerecek şekilde tutar.

## Tam çalışan örnek

Tüm parçaları bir araya getirerek, işte eksiksiz, çalıştırılabilir program:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Beklenen çıktı**: `output.xlsx` dosyasını Excel'de açın. **Copy** adlı bir sayfa göreceksiniz; A1:D20 hücreleri aynı veri, biçimlendirme ve orijinale aynı aktif pivot tabloyu içerir.

## Yaygın sorular ve uç durumlar

- **Kaynak aralık birleştirilmiş hücreler içeriyorsa ne olur?**  
  `copy` metodu birleştirme bilgilerini de kopyalar, böylece hedef sayfada birleştirilmiş hücreler değişmeden kalır.

- **Farklı bir çalışma kitabına kopyalayabilir miyim?**  
  Evet. İkinci bir `Workbook` örneği yükleyin, o çalışma kitabında bir hedef aralık oluşturun ve `sourceRange.copy(destinationRange)` metodunu çağırın. Metod, çapraz‑çalışma kitabı kopyalamayı otomatik olarak yönetir.

- **Hedef sayfada zaten veri varsa ne olur?**  
  Kopyalama işlemi, hedef aralıkla kesişen mevcut hücreleri üzerine yazar. Veri kaybını önlemek için hedef alanın boş olduğundan emin olun veya farklı bir başlangıç hücresi kullanın (ör. `"B2"`).

- **Pivot önbelleği çoğaltılıyor mu?**  
  Aspose.Cells, orijinal pivot önbelleğini yeniden kullanır; bu, yeni pivot tablonun aynı kaynak veriye bağlı kalması demektir. Bağımsız bir önbellek gerekiyorsa, kopyalamadan sonra pivot tabloyu yeniden oluşturmalısınız.

## İpuçları ve en iyi uygulamalar

- **Pro ipucu**: Aralığınız, kopyalanan bloğun dışındaki verilere bağımlı formüller içeriyorsa, kaydetmeden önce `Workbook.setForceFormulaRecalculation(true)` kullanın.
- **Dikkat edin** büyük aralıklar: devasa sayfaları kopyalamak önemli miktarda bellek tüketebilir. `OutOfMemoryError` alırsanız, daha küçük parçalar halinde kopyalamayı düşünün.
- **Performans ipucu**: Çok büyük dosyalarla çalışırken ekran güncellemeyi devre dışı bırakın (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) böylece kopyalama süresi hızlanır.

## Sonuç

Artık Aspose.Cells kullanarak sayfalar arasında **create new worksheet** ve **copy excel range** işlemlerini nasıl yapacağınızı, pivot tabloları ve tüm hücre özelliklerini koruyarak biliyorsunuz. Bu teknik, veri bloklarını programlı olarak çoğaltmanıza, rapor şablonları oluşturmanıza veya çalışma kitaplarını manuel kopyala‑yapıştır yapmadan yeniden yapılandırmanıza olanak tanır.

Sonra, çapraz‑çalışma kitabı işlemleri için **copy range aspose.cells**, pivot‑tablo yenilemelerini otomatikleştirme veya kopyalanan sayfayı PDF olarak dışa aktarma gibi ilgili konuları keşfedin. Belirli otomasyon senaryonuza uyacak şekilde farklı kaynak aralıkları ve sayfa adlarıyla denemeler yapın. İyi kodlamalar!

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}