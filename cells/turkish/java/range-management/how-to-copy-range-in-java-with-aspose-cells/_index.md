---
category: general
date: 2026-09-08
description: Aspose.Cells kullanarak Java’da aralığı nasıl kopyalarsınız – pivot tabloyu
  kopyalamayı, pivot tabloyu çoğaltmayı ve biçimlendirmeyi koruyarak pivot tabloyu
  dışa aktarmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: tr
lastmod: 2026-09-08
og_description: Aspose.Cells ile Java’da aralığı nasıl kopyalarsınız. Bu öğreticide,
  özet tabloyu nasıl kopyalayacağınızı, özet tabloyu nasıl çoğaltacağınızı ve biçimlendirmeyi
  koruyarak özet tabloyu nasıl dışa aktaracağınızı gösteriyoruz.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Java'da aralığı kopyalama – tam Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java'da Aspose.Cells ile aralığı nasıl kopyalarım
url: /tr/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells ile aralığı kopyalama

Java'da **aralığı nasıl kopyalanır** öğrenmek istiyorsanız, Aspose.Cells bu görevi basitleştirir. İster normal bir hücre bloğunu ister tam özellikli bir pivot tabloyu taşıyor olun, kütüphane kopyalama işlemini formülleri, stilleri ve pivot önbelleğini koruyarak gerçekleştirir. Bu rehberde **pivot tabloyu kopyala**, **pivot tabloyu çoğalt** ve hatta **pivot tabloyu dışa aktar** tam biçimlendirme ile yeni bir çalışma kitabına nasıl yapacağınızı öğreneceksiniz.

Bu öğretici, proje kurulumundan son doğrulama adımına kadar her şeyi kapsar, böylece okuduktan hemen sonra kodu çalıştırabilirsiniz. Aspose.Cells for Java JAR'ı dışında hiçbir dış araç gerekmemektedir.

## Önkoşullar

- Java 17 (veya desteklenen herhangi bir JDK) IDE'nizde yüklü ve yapılandırılmış.
- Bağımlılık yönetimi için Maven veya Gradle (örneklerde Maven kullanılmıştır).
- Aralık `A1:H20` içinde bir pivot tablo içeren bir kaynak Excel dosyası (`source.xlsx`).
- Java programlamaya temel aşinalık.

## Adım 1: Aspose.Cells'i projenize ekleyin

Aspose.Cells ticari bir kütüphanedir, ancak ücretsiz bir değerlendirme sürümü mevcuttur. `pom.xml` dosyanıza bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Gradle tercih ediyorsanız, eşdeğer giriş şudur:  
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

JAR'ı eklemek, bu rehber boyunca kullanılan `Workbook`, `Worksheet`, `Range` ve `CopyOptions` sınıflarına erişim sağlar.

## Adım 2: Kaynak çalışma kitabını yükleyin ve ilk çalışma sayfasını seçin

Aralığı kopyalamanın ilk aşaması, taşımak istediğiniz verileri içeren çalışma kitabını açmaktır.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Neden önemli:** Çalışma kitabını açmak, API'nin orijinal dosyaya dokunmadan bellekte bir temsil oluşturmasını sağlar.

## Adım 3: Pivot tabloyu içeren aralığı tanımlayın

Pivot tablo dikdörtgen bir blok içinde bulunur. Aspose.Cells'in neyi kopyalayacağını bilmesi için bu bloğu belirtmelisiniz.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Not:** `createRange` yöntemi henüz bir şey kopyalamaz; yalnızca çoğaltmak istediğiniz hücreleri işaret eden bir `Range` nesnesi oluşturur.

## Adım 4: Yeni bir çalışma kitabı oluşturun ve ilk çalışma sayfasını alın

Şimdi kopyalanan aralığın yer alacağı hedef çalışma kitabını oluşturun.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Neden yeni bir çalışma kitabı?** Yeni bir dosya kullanmak, gizli stillerin veya adlandırılmış aralıkların kopyalama işlemini etkilemesini önler; bu, pivot tabloyu ayrı bir dosyaya **dışa aktar** dığınızda özellikle önemlidir.

## Adım 5: Aralığı (pivot tablo dahil) hedef sayfaya kopyalayın

Bu, **biçimlendirme ile aralığı nasıl kopyalanır** konusunun özüdür. `CopyOptions` nesnesi, Aspose.Cells'e değerleri, formülleri, stilleri ve pivot önbelleğini korumasını söyler.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Pivot tabloyu kopyala:** Kaynak aralık pivot tabloyu içerdiği için API, pivot önbelleğini otomatik olarak çoğaltır; böylece yeni çalışma sayfası, orijinali gibi tam işlevsel bir pivot tablo içerir.

## Adım 6: Hedef çalışma kitabını kaydedin

Son olarak sonucu diske yazın.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

`dest.xlsx` dosyasını açtığınızda, orijinal pivot tablonun biçimlendirme, dilimleyiciler ve hesaplanmış alanlar dahil tam bir kopyasını göreceksiniz.

## Beklenen çıktı

- `dest.xlsx` dosyası **Sheet1** adlı bir çalışma sayfası içerir.
- `A1:H20` hücreleri kaynakla aynı veri ve pivot tabloyu tutar.
- Tüm hücre stilleri (yazı tipleri, renkler, kenarlıklar) korunur.
- Pivot tablo tamamen etkileşimlidir; yenilendiğinde kopyalanan aralıktaki temel verileri yansıtır.

## Aralığı biçimlendirme ile kopyalama – daha derin bir bakış

Önceki örnek en basit senaryoyu gösterir, ancak biraz farklı bir yaklaşım gerektiren varyasyonlarla karşılaşabilirsiniz.

### Pivot tabloyu mevcut bir çalışma kitabına kopyala

Bir çalışma kitabında zaten veri varsa **pivot tabloyu çoğalt**manız gerekiyorsa, aynı `copyRange` çağrısını kullanın ancak farklı bir hedef adresine işaret edin:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Sadece pivot tabloyu dışa aktar (çevresel veri olmadan)

Bazen sadece pivot tabloyu, kaynak veriyi istemezsiniz. Pivot tablonun görüntüleme aralığını `getPivotTable` yöntemiyle belirleyin:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Koşullu biçimlendirmeyi koru

Koşullu biçimlendirme kuralları stil koleksiyonunun bir parçasıdır. `PasteType.ALL` bayrağı zaten bunları kopyalar, ancak açıkça belirtebilirsiniz:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Kenar durumları ve sorun giderme

| Durum | Dikkat edilmesi gereken | Önerilen çözüm |
|-----------|-------------------|-----------------|
| Kaynak ve hedef çalışma kitapları farklı Excel sürümleri kullanıyor | Bazı yeni pivot özellikleri (ör. veri modeli) doğru görüntülenmeyebilir | Her iki çalışma kitabı için de en son Aspose.Cells sürümünü kullanın ve `Workbook.setFileFormatType(FileFormatType.XLSX)` ayarlayın |
| Çok büyük pivot tablolar ( > 10 000 satır) bellek baskısı oluşturur | Kopyalama sırasında bellek yetersizliği hataları | Yüklemeden önce `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` etkinleştirin |
| Hedef sayfa, kaynakla aynı ada sahip bir adlandırılmış aralık zaten içeriyor | İsim çakışması `CopyOptions` hatasına yol açar | `copyOptions.setIgnoreNameConflicts(true)` çağırın |

## Tam, çalıştırılabilir örnek

Aşağıda bir Java sınıfına kopyalayıp yapıştırabileceğiniz tam program yer almaktadır. Tüm import'ları, hata yönetimini ve yorumları içerir.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Programı çalıştırın, ardından `dest.xlsx` dosyasını açarak pivot tablonun orijinali gibi çalıştığını doğrulayın.

## Sonuç

Artık Aspose.Cells kullanarak Java'da **aralığı nasıl kopyalanır** bildiğinize, **pivot tabloyu kopyala**, **pivot tabloyu çoğalt** ve **pivot tabloyu dışa aktar** gibi işlemleri tüm biçimlendirmeyi koruyarak yapabildiğinize emin olabilirsiniz. Kütüphane, Excel'in XML yapısının düşük seviyeli detaylarını soyutlayarak iş mantığınıza odaklanmanızı sağlar.

### Sonraki adımlar

- Grafikler ve resimler için **biçimlendirme ile aralık kopyalama**'yı keşfedin (`PasteType.PICTURES` kullanın).
- Toplu işleme otomasyon: birden fazla kaynak dosyayı döngüye alıp pivot tablolarını özet bir çalışma kitabında birleştirin.
- Bu tekniği Aspose.Slides ile birleştirerek, kopyalanan pivotu gömülü PowerPoint raporları oluşturun.

## Sonraki Öğrenmeniz Gerekenler?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells – A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}