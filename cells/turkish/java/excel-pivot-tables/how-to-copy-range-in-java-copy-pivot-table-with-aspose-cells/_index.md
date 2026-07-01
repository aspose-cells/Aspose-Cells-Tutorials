---
category: general
date: 2026-06-30
description: Aspose.Cells kullanarak Java’da aralığı nasıl kopyalanır – Excel aralığını
  çoğaltma, pivot tabloyu kopyalama ve Excel çalışma kitabını verimli bir şekilde
  yükleme.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: tr
og_description: Aspose.Cells ile Java’da aralığı nasıl kopyalarsınız. Excel aralığını
  çoğaltmayı, pivot tabloyu kopyalamayı ve Excel çalışma kitabını dakikalar içinde
  yüklemeyi öğrenin.
og_title: Java'da aralık nasıl kopyalanır – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Java’da aralığı nasıl kopyalanır – Aspose.Cells ile Pivot Tablo kopyalama
url: /tr/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da aralık nasıl kopyalanır – Aspose.Cells ile Pivot Tablo Kopyalama

Bir Excel çalışma kitabından diğerine pivot tablo bütünlüğünü kaybetmeden **aralık nasıl kopyalanır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama sürecinde pivot mantığını korurken *excel aralığını çoğaltma* ihtiyacı günlük bir baş ağrısıdır. Neyse ki, Java için Aspose.Cells bunu çocuk oyuncağı haline getiriyor ve bu öğreticide, **Excel çalışma kitabını yükleme**, bir pivot tabloyu kopyalama ve sonucu kaydetme işlemlerini gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Bu rehberin sonunda, kendine özgü bir Java programına sahip olacaksınız:

* Mevcut bir çalışma kitabını yükler (`load excel workbook`);
* Pivot tabloyu içeren tam hücreleri tanımlar;
* Yeni bir çalışma kitabında **pivot table to sheet** öğesini kopyalar;
* Yeni dosyayı kaydeder, sonraki işlemler için hazır.

Harici betikler yok, manuel adımlar yok—sadece saf kod.

## Gereksinimler

Başlamadan önce, şunların olduğundan emin olun:

* Java 8 veya daha yeni bir sürüm (kod Java 11+ ile de çalışır);
* Aspose.Cells for Java kütüphanesi (Maven Central'dan edinebilirsiniz);
* İki örnek Excel dosyası – pivot tablo içeren bir kaynak (`source.xlsx`) ve `copy-pivot.xlsx` dosyasını yazacağınız bir hedef klasör.

Hepsi bu. Karmaşık IDE hilelerine gerek yok; herhangi bir metin düzenleyici ve `javac` yeterli.

## Adım 1: Projeyi Kurun ve Aspose.Cells'i İçe Aktarın

İlk iş olarak, kütüphaneyi projeye ekleyelim. Maven kullanıyorsanız, bu bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Maven kullanmıyorsanız, JAR dosyasını Aspose web sitesinden indirip sınıf yolunuza (classpath) ekleyin. Bu halledikten sonra, `CopyPivotDemo` adlı yeni bir Java sınıfı oluşturun.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro ipucu:** `src/main/java` klasörünüzü temiz tutun ve sınıfa anlamlı bir ad verin; bu gelecekteki bakımını kolaylaştırır.

## Adım 2: Kaynak Çalışma Kitabını Yükleyin (`load excel workbook`)

Şimdi, kopyalamak istediğimiz pivot tabloyu içeren **load excel workbook** işlemini gerçekleştiriyoruz. `Workbook` yapıcı (constructor) bir dosya yolu alır, bu yüzden yolun doğru olduğundan emin olun.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Neden ilk çalışma sayfasını seçiyoruz? Çoğu basit durumda pivot ilk sayfada bulunur, ancak gerektiğinde indeksi değiştirebilir veya sayfa adını kullanabilirsiniz. Bu esneklik, Aspose.Cells'in öne çıkan özelliklerinden biridir.

## Adım 3: Pivot Tabloyu İçeren Aralığı Tanımlayın

Bir pivot tablo genellikle bir hücre bloğunu kapsar. `A1:G20` aralığını kullandığını varsayalım. Gerçek verinize uygun olacak şekilde adresi ayarlayabilirsiniz.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Tam adresi bilmiyorsanız, çalışma kitabını Excel'de açın, tüm pivotu seçin ve ad kutusuna bakın. Unutmayın, **duplicate excel range** en iyi, tam alanı hedeflediğinizde çalışır—ekstra satır yok, eksik sütun yok.

## Adım 4: Hedef İçin Yeni Bir Çalışma Kitabı Oluşturun

Kopyalanan aralığı alacak yeni bir çalışma kitabına ihtiyacımız var. Burada **copy pivot table** yeni bir sayfaya yapılacak.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Bu noktada hedef çalışma kitabı boş, ancak Aspose.Cells otomatik olarak bir varsayılan sayfa ekler; bunu hedef olarak kullanacağız.

## Adım 5: Aralığı Kopyalayın – Pivot Tablo Aynı Kalır

İşte **copy pivot table** yaparken tüm iç bağlantılarını koruyan sihirli satır.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

`copy` yöntemi iki argüman alır: kaynak `Range` ve hedef `Range`. Hedefi `A1`'den başlatarak, pivotu kaynakta olduğu gibi yerleştiririz. Aspose.Cells, temel pivot önbelleğini kopyalar, böylece yeni çalışma kitabı pivotu nasıl yenileyeceğini hâlâ bilir.

## Adım 6: Oluşan Çalışma Kitabını Kaydedin

Son olarak, yeni dosyayı diske yazın. Aspose'un desteklediği herhangi bir formatı seçebilirsiniz (`.xlsx`, `.xls`, `.csv`, vb.). Biz `.xlsx` formatını kullanacağız.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Programı çalıştırın, aynı pivot düzenine sahip yeni bir çalışma kitabı görmelisiniz. Excel'de açın—her şey yolunda ise, pivotu hatasız bir şekilde yenileyebileceksiniz.

### Beklenen Çıktı

`CopyPivotDemo` çalıştırdığınızda, konsol şu çıktıyı verir:

```
Pivot table successfully copied to copy-pivot.xlsx
```

`copy-pivot.xlsx` dosyasını açtığınızda, kaynağın pivot alanına tamamen aynı görünen bir sayfa ortaya çıkar ve **pivot table to sheet** orijinali gibi çalışır.

## Tam Çalışan Örnek

Aşağıda, tüm adımları birleştiren tam, çalıştırılabilir Java sınıfı bulunmaktadır. IDE'nize kopyalayıp yapıştırın, dosya yollarını ayarlayın ve çalıştırın.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Not:** Pivot tablonuz birden fazla çalışma sayfasını kapsıyorsa, ilgili her sayfa için kopyalama adımını tekrarlayın veya tüm çalışma sayfalarını klonlamak için `Workbook.copy` kullanın.

## Yaygın Sorular ve Kenar Durumları

### Kaynak çalışma kitabının birden fazla çalışma sayfası olması durumunda ne olur?

`sourceWorkbook.getWorksheets()` üzerinden döngü kurarak ilgili her aralığı kopyalayabilirsiniz. Referansları korumanız gerekiyorsa, hedefte aynı sayfa adlarını tutmaya özen gösterin.

### Kopyalanan pivot veri kaynağını korur mu?

Evet. Aspose.Cells, aralıkla birlikte pivot önbelleğini de kopyalar, bu yüzden hedef çalışma kitabı aynı dosya içindeki orijinal veri kaynağına hâlâ işaret eder. Daha sonra veriyi farklı bir sayfaya taşırsanız, pivotu manuel olarak yenilemeniz gerekebilir.

### Harici bir veri kaynağı kullanan pivot nasıl kopyalanır?

Pivotun veri kaynağı harici bir dosya olduğunda, pivotu kopyalamadan önce bu veriyi hedef çalışma kitabına (örneğin, kaynak veri aralığını kopyalayarak) eklemeniz gerekir. Aksi takdirde pivot “#REF!” hataları verir.

### Pivotu çevresindeki veriler olmadan kopyalayabilir miyim?

Kesinlikle. `pivotRange`i sadece pivotun hücrelerini kapsayacak şekilde ayarlayın (genellikle sol‑üst köşe ve veri alanı). Ayrıca programatik olarak tam aralığı elde etmek için `sourceSheet.getPivotTables().get(0).getPivotTableArea()` kullanabilirsiniz.

## Gerçek‑Dünya Projeleri İçin İpuçları

* **Batch processing:** Onlarca çalışma kitabını çoğaltmanız gerekiyorsa, yukarıdaki kodu bir metoda sarın ve bir dizinde dönen bir döngü içinde çağırın.
* **Performance:** Büyük dosyalar için tek bir `Workbook` örneğini yeniden kullanın ve tüm kopyalar tamamlandıktan sonra `Workbook.calculateFormula()` metodunu çağırın.
* **Error handling:** Kopyalama mantığını try‑catch bloklarıyla sarın ve `Exception.getMessage()`'ı loglayın; geçersiz aralıklar için Aspose `CellsException` fırlatır.

## Sonuç

Aspose.Cells kullanarak Java’da **how to copy range** konusunu ele aldık, size **duplicate excel range**, **copy pivot table** ve **load excel workbook** işlemlerini tek bir düzenli programda nasıl yapacağınızı gösterdik. Adımlar basit, kod tamamen çalıştırılabilir ve yaklaşım tek sayfalık bir demodan kurumsal seviyedeki toplu işlere kadar ölçeklenebilir.

Bir sonraki zorluğa hazır mısınız? Kopyalanan pivotu PDF olarak dışa aktarmayı deneyin ya da yeni veri ekledikten sonra programatik olarak yenileyin. Her iki görev de burada oluşturduğumuz temele dayanır, böylece onları rahatlıkla ele alabilirsiniz.

Sorularınız mı var ya da kendi düzenlemelerinizi paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın—mutlu kodlamalar!

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose.Cells Java’da Çalışma Kitabı Kapsamı ile Adlandırılmış Aralık Nasıl Uygulanır – Gelişmiş Excel Veri Yönetimi](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Aspose.Cells Java Kullanarak Excel’de Birden Fazla Sütunu Kopyalama: Tam Kılavuz](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Aralık Verisini Kopyalama](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}