---
category: general
date: 2026-08-17
description: Aspose.Cells kullanarak Java’da çalışma sayfasını nasıl çoğaltılır, pivot
  tablo korunarak, pivot yeni bir çalışma kitabına kopyalanır ve bir sayfadan çalışma
  kitabı oluşturulur.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: tr
lastmod: 2026-08-17
og_description: Aspose.Cells kullanarak Java’da çalışma sayfasını nasıl kopyalarsınız,
  pivot tabloyu koruyarak, pivotu yeni bir çalışma kitabına kopyalar ve bir sayfadan
  çalışma kitabı oluşturur—tüm adımlar açıklanmıştır.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Çalışma sayfasını nasıl çoğaltır ve pivot tablolarını korursunuz – Java
  rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Java'da çalışma sayfasını nasıl çoğaltır ve pivot tablolarını korursunuz
url: /tr/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Çalışma Sayfasını Kopyalama ve Pivot Tablolarını Korumak

Çalışma sayfasını pivot tablosu bozulmadan kopyalamak, Excel raporlamasını otomatikleştirdiğinizde sık karşılaşılan bir ihtiyaçtır. Bu kılavuz, Aspose.Cells for Java kullanarak pivotu yeni bir çalışma kitabına nasıl kopyalayacağınızı gösterir ve ayrıca bir çalışma sayfasından çalışma kitabı oluştururken pivotu nasıl koruyacağınızı ele alır.

Mevcut bir çalışma kitabını nasıl yükleyeceğinizi, pivot tablosu içeren çalışma sayfasını nasıl kopyalayacağınızı ve sonucu yeni bir dosya olarak nasıl kaydedeceğinizi öğreneceksiniz. Eğitim, temel bir Java geliştirme ortamına ve geçerli bir Aspose.Cells lisansına (ücretsiz değerlendirme testi için çalışır) sahip olduğunuzu varsayar. Aspose.Cells JAR dışındaki hiçbir dış araç gerekmemektedir.

## Önkoşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

* Java Development Kit (JDK) 8 veya daha yeni bir sürüm.
* Aspose.Cells bağımlılığını yönetmek için Maven veya Gradle.
* İlk çalışma sayfasında en az bir pivot tablo içeren bir Excel dosyası (`source.xlsx`).
* Kaynak dosyayı okuyup kopyalanan çalışma kitabını yazabileceğiniz bir dizin.

Aspose.Cells bağımlılığını `pom.xml` (Maven) veya `build.gradle` (Gradle) dosyanıza ekleyin. Maven için:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Pivot Tablosu ile Çalışma Sayfasını Kopyalama

Temel işlem üç adımlı bir süreçtir: yükleme, kopyalama ve kaydetme. Her adım aşağıda açıklanmıştır.

### Adım 1 – Pivot tablosunu içeren çalışma kitabını yükleme

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Neden bu adım önemlidir*: `Workbook` nesnesi tüm Excel dosyasını temsil eder. İlk çalışma sayfasını (`get(0)`) alarak, kopyalamak istediğiniz pivot tablosunu içeren sayfayı hedeflersiniz.

### Adım 2 – Yeni bir çalışma kitabı oluşturma ve tüm çalışma sayfasını kopyalama

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` çalışma sayfasını **tüm gömülü nesneler, formüller ve pivot önbellekleri** dahil olmak üzere klonlar. Bu, **pivotun nasıl kopyalanacağı** için önerilen yoldur çünkü pivot tanımı ve veri kaynağı birlikte aktarılır.

### Adım 3 – Yeni çalışma kitabını kaydetme

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Çalıştırdıktan sonra, `copy_with_pivot.xlsx` orijinal sayfanın tam bir kopyasını içerir ve pivot tablosu ek yapılandırma olmadan çalışır.

**Beklenen sonuç**: `copy_with_pivot.xlsx` dosyasını Excel'de açtığınızda, kaynak dosyayla aynı pivot düzeni, filtreler ve hesaplanmış alanlara sahip kopyalanmış çalışma sayfası gösterilir.

## Pivotu Başka Bir Çalışma Kitabına Kopyalama

Tam sayfayı kopyalamadan bir pivot tablosunu taşımak istiyorsanız, pivot önbelleğini çıkarıp yeni bir çalışma sayfasına ekleyebilirsiniz. Aşağıdaki kod parçacığı bu yaklaşımı gösterir:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Bu kod, **pivotun nasıl kopyalanacağı** sorusuna sadece pivot nesnesini kopyalayarak yanıt verir, tüm çalışma sayfasını değil. `PivotTables` koleksiyonundaki `addCopy` yöntemi, pivot önbelleğinin kopyalanmasını sağlar ve **pivotun nasıl korunacağı** gereksinimlerini karşılar.

## Çalışma Sayfasından Çalışma Kitabı Oluştururken Pivotu Korumak

Bazen bir çalışma sayfası, bir çalışma kitabına ait değildir (örneğin, bellekte bir sayfa oluşturursunuz). Pivotu koruyarak **çalışma sayfasından çalışma kitabı oluşturmak** için aşağıdaki adımları izleyin:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Pivot tamamen tanımlandıktan sonra çalışma sayfasını yeni bir `Workbook` içine ekleyerek, **pivotun nasıl korunacağı** mevcut bir dosyanın dışından gelmiş olsa bile çalışır garantilenir.

## Pratik İpuçları ve Yaygın Tuzaklar

| İpucu | Neden önemli |
|-------|--------------|
| `addCopy` yerine `copy` kullanın | `addCopy` temel pivot önbelleğini klonlar; basit bir `copy` veri kaynağı bağlantısını kaybedebilir. |
| Kaynak ve hedef dosyaları aynı dosya sisteminde tutun | Pivotun veri kaynağındaki göreceli yollar doğru çözülür, “kaynak bulunamadı” hataları azalır. |
| Kopyalama sonrası pivot önbelleğini doğrulayın | Kopyalama ve kaydetme işlemleri arasında kaynak veri değiştiyse `pivot.refresh()` çağırın. |
| İşiniz bittiğinde çalışma kitaplarını serbest bırakın | `sourceWorkbook.dispose();` yerel kaynakları serbest bırakır, büyük dosyalar için önemlidir. |

## Karşılaşabileceğiniz Kenar Durumları

* **Birbirine bağımlı birden fazla pivot içeren çalışma sayfaları** – Her çalışma sayfasını ayrı ayrı kopyalayın; paylaşılan önbellekler otomatik olarak çoğaltılır, ancak dış veri bağlantılarını yeniden atamanız gerekebilir.  
* **Harici SQL sorgularına dayalı pivot tablolar** – Hedef ortamın aynı veritabanına erişebildiğinden emin olun; aksi takdirde pivot “#REF!” hataları gösterir.  
* **Büyük çalışma kitapları (>100 MB)** – Kopyalama sırasında bellek baskısını azaltmak için `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` kullanın.

## Tam, Çalıştırılabilir Örnek

Aşağıda tartışılan tüm adımları içeren tam program yer almaktadır. `CopyPivotTable.java` olarak kaydedin, dosya yollarını ayarlayın ve tercih ettiğiniz IDE ile ya da `javac`/`java` komutlarıyla çalıştırın.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java Kullanarak Excel'de Pivot Tabloları Oluşturma: Kapsamlı Rehber](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Pivot Tablosu Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java ile Pivot Tablolarında Dilimleyicileri Uygulama: Kapsamlı Rehber](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}