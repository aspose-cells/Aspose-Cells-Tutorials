---
category: general
date: 2026-07-23
description: Java'da yeni bir çalışma kitabı oluşturun ve dakikalar içinde Aspose.Cells
  ile özet tabloyu kopyalamayı, Excel aralığını kopyalamayı ve özet tabloyu dışa aktarmayı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: tr
lastmod: 2026-07-23
og_description: Java'da yeni bir çalışma kitabı oluşturun ve pivot tabloyu anında
  kopyalayın, Excel aralığını kopyalayın, ardından Aspose.Cells kullanarak pivot tabloyu
  dışa aktarın. Bu eksiksiz öğreticiyi izleyin.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Java'da Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Adım Adım Kopyala
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Java'da Yeni Çalışma Kitabı Oluşturma – Pivot Tablosunu Kopyalama Tam Kılavuzu
url: /tr/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Yeni Çalışma Kitabı Oluşturma – Pivot Tablosunu Kopyalama İçin Tam Kılavuz

Karmaşık bir pivot tablosunu korurken Java'da **yeni bir çalışma kitabı** oluşturmanın nasıl yapılacağını hiç merak ettiniz mi? Bu konuda yalnız değilsiniz. Birçok raporlama uygulamasında bir pivotu kaynak dosyadan yeni bir çalışma kitabına taşımak gerekir; belki müşteriye göndermek ya da daha fazla hesaplama yapmak için. İyi haber? Birkaç satır kodla bunu tam olarak yapabilirsiniz—manuel kopyala‑yapıştırmaya gerek kalmadan.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: kaynak dosyayı yükleme, pivotun bulunduğu aralığı tanımlama, **Excel aralığını kopyalama**, **yeni bir çalışma kitabı** oluşturma ve sonunda **pivot tablosunu dışa aktarma**. Sonuna geldiğinizde, “**pivot nasıl kopyalanır**” sorusuna tahmin yürütmeden cevap veren, bağımsız ve çalıştırılabilir bir Java programına sahip olacaksınız.

## Gereksinimler

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Java 17 veya daha yeni bir sürüm (kod, herhangi bir güncel JDK ile çalışır)
- Aspose.Cells for Java kütüphanesi (ücretsiz deneme veya lisanslı sürüm)
- `source.xlsx` adlı, `A1:G20` aralığında bir pivot tablo içeren örnek dosya
- Aspose.Cells JAR dosyasını yönetebilecek bir IDE veya derleme aracı (Maven/Gradle)

Hepsi hazır mı? Harika—başlayalım.

## 1. Adım: Projeyi Kurun ve Aspose.Cells'i İçe Aktarın

İlk olarak, Aspose.Cells'i projenize eklemeniz gerekiyor. Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri şu şekildedir:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Kütüphane sınıf yoluna eklendikten sonra, ihtiyacınız olan sınıfları içe aktarın:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro ipucu:** Aspose.Cells ticari bir kütüphanedir, ancak çıktıya bir filigran ekleyen tam işlevsel 30‑günlük bir değerlendirme sürümü sunar—denemek için mükemmel.

## 2. Adım: Kaynak Çalışma Kitabını Yükleyin

Şimdi **yeni bir çalışma kitabı** nesneleri oluşturacağız, ancak önce pivotu içeren kaynağa ihtiyacımız var. Bu adım, **excel aralığını kopyala** işleminin temeli çünkü aralık nesnesi, pivot önbelleği dahil hangi hücrelerin aktarılacağını tam olarak bilir.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Aralığı doğrudan okumak neden mümkün değil? Çünkü pivot tablosunun meta verileri, çalışma sayfasının pivot önbelleğinde saklanır ve Aspose.Cells, aralığı kopyaladığınızda bunu otomatik olarak paketler.

## 3. Adım: Pivot Tablosunu İçeren Aralığı Tanımlayın

Gerçek dünyadaki birçok dosyada pivot, dikdörtgen bir blok olarak bulunur. Bu örnek için `A1:G20` aralığında olduğunu varsayacağız. Elbette, gerçek düzeninize göre adresi ayarlayabilirsiniz.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Tam adresi bilmiyorsanız, `sourceSheet.getCells().getMaxDataRow()` ve `getMaxDataColumn()` metodlarını kullanarak sınırları dinamik olarak hesaplayabilirsiniz. Pivot boyutu zaman içinde değiştiğinde bu oldukça kullanışlı bir yöntemdir.

## 4. Adım: **Yeni Çalışma Kitabı** Oluşturun ve Hedef Çalışma Sayfasını Hazırlayın

İşte **yeni bir çalışma kitabı** oluşturup kopyalanan içeriği alacak boş tuvali hazırladığımız an. Bunu, pivotu yapıştıracağınız boş bir kanvas olarak düşünün.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Neden boş bir çalışma kitabıyla başlıyoruz? Böylece gizli stiller veya önceki pivotlar kopyalamayı etkilemez; **pivot tablosunu dışa aktar** için temiz bir sonuç elde edersiniz.

## 5. Adım: Pivot Tablosunu (ve Altındaki Aralığı) Kopyalayın

Şimdi öğreticinin özü: **pivot tablosunu kopyala**. Aspose.Cells, bir aralık kopyasını derin bir kopya olarak ele alır; yani pivot önbelleği hücrelerle birlikte taşınır. Bu yüzden tek bir satır, işi halleder.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

**pivot nasıl kopyalanır** sorusunu hiç merak ettiyseniz, işte cevabı. Hedef sayfa artık tamamen çalışan bir pivot içeriyor; yenileyebilir, değiştirebilir veya doğrudan dışa aktarabilirsiniz.

### Kenar Durumu: Yenileme Ayarlarını Korumak

Bazen kaynak pivot, açıldığında yenilenmek üzere ayarlanmıştır. Bu davranışı korumak için pivotun seçeneklerini açıkça kopyalayabilirsiniz:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Bu kod parçacığı, kopyalanan pivotun orijinaliyle aynı şekilde çalışmasını sağlar.

## 6. Adım: Hedef Çalışma Kitabını Kaydedin – **Pivot Tablosunu Dışa Aktarın**

Son olarak, yeni çalışma kitabını diske kaydederek **pivot tablosunu dışa aktar**acağız. Aspose'un desteklediği herhangi bir formatı seçebilirsiniz: XLSX, XLS, CSV, PDF vb. Bu kılavuzda XLSX formatını kullanacağız.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Dosyayı bir web servisine göndermeniz gerekiyorsa, dosya yolunu kullanmak yerine bir `ByteArrayOutputStream`'a yazabilirsiniz—Aspose bunu çok basit hale getirir.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, işte eksiksiz, çalıştırılabilir bir program. Kopyalayıp IDE'nizde yapıştırarak çalıştırabilirsiniz.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda konsola şu mesaj yazdırılır:

```
Pivot table copied successfully!
```

Ve `copied_with_pivot.xlsx` dosyası `YOUR_DIRECTORY` içinde oluşur. Excel'de açtığınızda pivot tablosunun eksiksiz olduğunu, yenilenmeye ya da düzenlemeye hazır olduğunu göreceksiniz.

## Yaygın Sorular & Sorun Giderme

- **Kaynak pivot birden fazla çalışma sayfasına yayılmışsa ne olur?**  
  İlgili her aralığı ayrı ayrı kopyalamanız, ardından `PivotTable` API'lerini kullanarak hedef sayfada pivotu yeniden oluşturmanız gerekir.

- **Sadece pivot düzenini, verileri kopyalamadan alabilir miyim?**  
  Kopyalamadan önce `sourceRange.setCopyDataOnly(false)` ayarlayın. Bu, Aspose'a önbelleği tutmasını ama temel veri setini kopyalamamasını söyler.

- **Pivotu bir CSV dosyasına kopyalamanın bir yolu var mı?**  
  CSV pivotları desteklemez, ancak `pivotTable.calculate()` çağırıp ardından sayfayı CSV olarak kaydederek pivotun *sonucunu* dışa aktarabilirsiniz.

- **Kopyalanan pivot biçimlendirmesini kaybediyor, neden?**  
  Biçimlendirme stil koleksiyonunda saklanır. Kopyalama sonrası `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` çağırarak stilleri aktarabilirsiniz.

## Sonuç

Java'da **yeni bir çalışma kitabı** oluşturmayı, **pivot tablosunu kopyalamayı** ve **pivot tablosunu dışa aktarmayı**—tamamen temiz, yeniden üretilebilir bir kod örneğiyle gösterdik. **excel aralığını kopyala** işlemini doğru tanımlayarak, Aspose.Cells'in derin‑kopya semantiğinden yararlanarak ve isteğe bağlı ayarları koruyarak neredeyse her pivot‑taşıma görevini otomatikleştirebilirsiniz.

Bir sonraki adıma hazır mısınız? Çıktı formatını PDF'ye dönüştürmeyi deneyin ya da birden çok kaynak dosyası üzerinde döngü kurarak onlarca pivotu toplu işleyin. Aynı desen geçerli—sadece dosya yollarını ve aralık adreslerini ayarlamanız yeterli.

Bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da gelişmiş pivot manipülasyonu için Aspose.Cells belgelerine göz atın. Kodlamanın tadını çıkarın ve bu sıkıcı kopyala‑yapıştırma işlerini otomatikleştirerek kazandığınız zamanı değerlendirin!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakın konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve API özelliklerini daha iyi kavramanıza ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}