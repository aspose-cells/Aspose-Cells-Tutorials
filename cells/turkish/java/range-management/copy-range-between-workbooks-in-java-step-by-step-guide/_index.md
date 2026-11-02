---
category: general
date: 2026-08-14
description: Aspose.Cells kullanarak Java ile çalışma kitapları arasında aralık kopyalama.
  Pivot tablo çalışma kitabını kopyalamayı, resmi PowerPoint’e aktarmayı ve Excel
  tablosundan AutoFilter’ı kaldırmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: tr
lastmod: 2026-08-14
og_description: Java'da çalışma kitapları arasında aralık kopyalama. Bu kılavuz, pivot
  tablo çalışma kitabını kopyalamayı, resmi PowerPoint'e dışa aktarmayı ve Excel tablosundan
  Otomatik Filtreyi kaldırmayı gösterir.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Java'da çalışma kitapları arasında aralığı kopyala – tam Aspose.Cells öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Java'da çalışma kitapları arasında aralık kopyalama – adım adım rehber
url: /tr/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Çalışma Kitapları Arasında Aralık Kopyalama – adım adım kılavuz

Java’da **copy range between workbooks** işlemini yapmanız gerekiyorsa, Aspose.Cells karmaşık nesneler (pivot tablolar ve resimler gibi) ile başa çıkabilen temiz bir API sunar. Bu öğreticide **copy pivot table workbook**, **export picture to PowerPoint** ve **remove AutoFilter from Excel table** nasıl yapılır gösterilir ve kodun okunması ve bakımı kolay tutulur.

Aşağıdakileri öğreneceksiniz:

* Kaynak bir çalışma kitabını yükleyin ve kaynak aralığı tanımlayın.  
* Hedef bir çalışma kitabı oluşturun ve aralığı kopyalayın, böylece pivot tablo bozulmaz.  
* Sayfadaki ilk resmi düzenlenebilir bir PowerPoint nesnesi olarak dışa aktarın.  
* İlk Excel tablosundan AutoFilter'ı kaldırın.  
* `SmartMarkerOptions` ile bir çalışma kitabı yükleyin ve JSON dizilerini tek bir hücre değeri olarak işleyin.

Örnek, Java için Aspose.Cells 23.10 kullanır, ancak kavramlar daha eski sürümlerde de geçerlidir.

---

## Önkoşullar

| Gereksinim | Neden Önemlidir |
|-------------|----------------|
| Java 17 veya daha yeni | En son Aspose.Cells çalışma zamanı tarafından gereklidir. |
| Aspose.Cells for Java (Maven artefaktı `com.aspose:aspose-cells`) | Kodda kullanılan `Workbook`, `Worksheet`, `Range` ve ilgili sınıfları sağlar. |
| Pivot tablo, resim ve AutoFilter içeren bir kaynak Excel dosyası (`src.xlsx`). | Bu öğretici, bu nesneleri manipüle ederek her özelliği gösterir. |

Maven bağımlılığını `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Çalışma Kitapları Arasında Aralık Kopyalama – kaynak ve hedefi yükleme

İlk adım, kaynak çalışma kitabını açmak, kopyalamak istediğiniz verileri içeren aralığı seçmek ve boş bir hedef çalışma kitabı oluşturmaktır.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Neden bu önemli:** `Range.copy` kullanılarak, Aspose.Cells yalnızca ham hücre değerlerini değil, aynı zamanda temel pivot önbelleğini de kopyalar ve pivot tablonun hedef çalışma kitabında işlevsel kalmasını sağlar.

---

## Aralığı kopyalarken pivot tablo çalışma kitabını kopyala

Şimdi tanımlanan aralığı kaynak çalışma kitabından hedef çalışma kitabına kopyalayın. Aralık pivot önbelleğini içerdiği için pivot tablo otomatik olarak korunur.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Sonuç:** `destination.xlsx` dosyasını açtığınızda `src.xlsx` ile aynı pivot tablo düzeni gösterilir. Pivot önbelleğini yeniden oluşturmak için ek bir koda gerek yoktur.

---

## Resmi PowerPoint’e Dışa Aktar

Aspose.Cells bir resmi düzenlenebilir bir PowerPoint nesnesi olarak dışa aktarmak için işaretleyebilir. Aşağıdaki kod, hedef sayfadaki ilk resmi seçer ve dışa aktarma bayrağını ayarlar.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Gördükleriniz:** `destination.pptx` dosyasını PowerPoint’te açtığınızda resim, düzenleyebileceğiniz, yeniden boyutlandırabileceğiniz veya animasyon ekleyebileceğiniz yerel bir şekil olarak gösterilir.

---

## Excel tablosundan AutoFilter’ı kaldır

Kaynak sayfa bir AutoFilter içeren bir tablo içeriyorsa, kopyaladıktan sonra bunu temizlemek isteyebilirsiniz. Aşağıdaki kod ilk tabloya erişir ve filtresini kaldırır.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Etkisi:** Tablo çalışma kitabında kalır, ancak açılır filtre okları kaybolur ve size temiz bir veri görünümü sağlar.

---

## SmartMarker seçenekleriyle çalışma kitabı yükleme – JSON dizilerini tek bir hücre olarak işleme

JSON’den rapor oluştururken, Aspose.Cells bir bütün diziyi tek bir hücre değeri olarak ele alabilir. Bu, JSON dizelerini bir şablona birden fazla hücreye genişletmeden gömmek için kullanışlıdır.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Neden bunu kullanabilirsiniz:** JSON yükünüzde tek bir hücrede JSON dizesi olarak görünmesi gereken bir dizi varsa, `setArrayAsSingle(true)` Aspose.Cells’in diziyi ayrı satır veya sütunlara genişletmesini engeller.

![Java’da Çalışma Kitapları Arasında Aralık Kopyalama – Aspose.Cells kod örneği](copy-range-workbooks.png)

*Görsel alt metni:* **Java’da Çalışma Kitapları Arasında Aralık Kopyalama – Aspose.Cells kod örneği** (anahtar kelimeyle eşleşir).

---

## Beklenen çıktı

| Dosya adı                | İçerik |
|--------------------------|--------|
| `destination.xlsx`       | Fonksiyonel pivot tablo ile kopyalanan aralık. |
| `destination.pptx`       | Dışa aktarılan resim, düzenlenebilir bir PowerPoint şekli olarak. |
| `final_output.xlsx`      | AutoFilter okları olmayan tablo. |
| `template_filled.xlsx`   | Tek bir hücre değeri olarak saklanan JSON dizisi. |

Her dosyayı ilgili uygulamada (Excel veya PowerPoint) açarak işlemlerin başarılı olduğunu doğrulayın.

---

## Sonuç

Artık Aspose.Cells kullanarak Java’da **copy range between workbooks** nasıl yapılacağını biliyorsunuz; pivot tabloyu koruyarak, resmi PowerPoint’e dışa aktararak ve Excel tablosundan AutoFilter’ı kaldırarak. Aynı desen, herhangi bir Excel aralığını yeni bir çalışma kitabına kopyalamak, SmartMarker JSON dizilerini işlemek veya ek dönüşümler zinciri oluşturmak için genişletilebilir.

Keşfedebileceğiniz sonraki adımlar:

* **Copy Excel range to new workbook** birden fazla çalışma sayfası ile.  
* **export picture to PowerPoint**'i toplu resim çıkarımı için kullanın.  
* Büyük raporlama hatlarında **remove autofilter from excel table** uygulayın.  
* Bu teknikleri Aspose.Slides ile birleştirerek tam Excel‑to‑PowerPoint otomasyonu sağlayın.

Farklı aralık adresleri, birden fazla pivot tablo veya özel resim formatlarıyla denemeler yapmaktan çekinmeyin. Aspose.Cells API, programatik esneklik için tasarlanmıştır; bu yüzden burada gösterilen desenleri herhangi bir kurumsal Excel otomasyon senaryosuna uyarlayabilirsiniz.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Aspose.Cells for Java Kullanarak Excel’de Sayfalar Arası Görüntü Kopyalama: Kapsamlı Kılavuz](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Aspose.Cells Java Kullanarak Excel’de Çalışma Sayfaları Arasında Sayfa Ayarı Kopyalama](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Çalışma Kitapları Arasında Çalışma Sayfalarını Kopyalama](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}