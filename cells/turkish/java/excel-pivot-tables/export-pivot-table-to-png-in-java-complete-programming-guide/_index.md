---
category: general
date: 2026-06-27
description: Java'da pivot tabloyu Excel pivot görüntüsü olarak dışa aktarın. PNG
  formatını nasıl ayarlayacağınızı, seçenekleri nasıl yapılandıracağınızı ve dosyayı
  sadece birkaç adımda nasıl kaydedeceğinizi öğrenin.
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: tr
og_description: Java kullanarak pivot tablosunu Excel pivot görüntüsü olarak dışa
  aktarın. Bu kılavuz, PNG formatını ayarlamayı ve görüntüyü güvenle kaydetmeyi gösterir.
og_title: Java'da Pivot Tablosunu PNG Olarak Dışa Aktarma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Java’da Pivot Tablosunu PNG Olarak Dışa Aktarma – Tam Programlama Rehberi
url: /tr/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Pivot Tablosunu PNG Olarak Dışa Aktarma – Tam Programlama Rehberi

Hiç **pivot tablosunu** bir Excel çalışma kitabından dışa aktarmanız gerekti ama temiz bir görüntü dosyası elde etmenin nasıl yapılacağından emin olmadınız mı? Tek başınıza değilsiniz—birçok geliştirici raporlama panoları oluştururken bu engelle karşılaşıyor. İyi haber şu ki, birkaç satır Java kodu ile herhangi bir pivot tabloyu net bir **Excel pivot görüntüsü** olarak PNG formatında kaydedebilirsiniz.  

Bu öğreticide tüm süreci adım adım inceleyeceğiz: çalışma kitabını okuma, ilk pivot tabloyu bulma, dışa aktarmayı **PNG formatı ayarlama** için yapılandırma ve sonunda görüntüyü diske yazma. Sonunda, herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Neler Öğreneceksiniz

- Aspose.Cells (veya tercih ederseniz Apache POI) ile bir Excel dosyasını nasıl yükleyeceğinizi.  
- **pivot tablosunu** PNG olarak dışa aktarmak için gereken kesin API çağrılarını.  
- Görüntü formatını ayarlamanın neden önemli olduğunu ve **PNG formatını** doğru şekilde nasıl ayarlayacağınızı.  
- Yaygın tuzaklar—birden fazla pivot tabloyu işlemek veya eksik çalışma sayfaları gibi—ve bunlardan nasıl kaçınılacağını.  
- Kopyala-yapıştır yapabileceğiniz tam, çalıştırılmaya hazır bir Java örneği.  

> **Önkoşullar**  
> • Java 17 veya daha yeni (kod daha eski sürümlerde de çalışır, ancak 17 önerilir).  
> • Aspose.Cells for Java kütüphanesi (ücretsiz deneme sürümü yeterli).  
> • Excel dosyaları ve Java I/O konusunda temel bilgi.  

## Adım 1: Aspose.Cells Bağımlılığını Ekleyin

Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin. Aksi takdirde, Aspose web sitesinden JAR dosyasını indirip sınıf yolunuza ekleyin.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* Beklenmedik hatalardan kaçınmak için kütüphane sürümlerinizi resmi sürüm notlarıyla senkronize tutun.

## Adım 2: Çalışma Kitabını Yükleyin ve Pivot Tablosunu Bulun

Önce Excel dosyasını açıyoruz, ardından ilk çalışma sayfasındaki ilk pivot tabloyu alıyoruz. Çalışma kitabı hiç pivot tablo içermiyorsa, sorunsuz bir şekilde çıkıyoruz.

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Bu adımın önemi** – `PivotTable` nesnesi herhangi bir görüntü dışa aktarmanın giriş noktasıdır. Var olmayan bir pivot üzerinde `toImage` çağırmaya çalışmak `NullPointerException` hatası verir, bu yüzden önce sayıyı kontrol ediyoruz.

## Adım 3: Görüntü Dışa Aktarma Seçeneklerini Yapılandırın (PNG Formatını Ayarlayın)

Şimdi bir `ImageOrPrintOptions` örneği oluşturup açıkça **PNG formatını ayarlıyoruz**. PNG kayıpsızdır ve ızgara çizgileri ile yazı tiplerinin keskinliğini korur.

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Not:* JPEG gerekiyorsa, sadece `ImageFormat.PNG` yerine `ImageFormat.JPEG` yazın. Aynı seçenek nesnesi her iki format için de çalışır.

## Adım 4: Pivot Tablosunu Görüntü Dosyası Olarak Dışa Aktarın

Seçenekler hazır olduğunda `toImage` metodunu çağırıyoruz. Metod dosyayı doğrudan yazar, bu yüzden ekstra akışlara ihtiyaç yoktur.

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Programı çalıştırdığınızda Excel'de gördüğünüz pivotla aynı görünüme sahip `pivot.png` adlı bir dosya oluşturulur. Doğrulamak için herhangi bir görüntü görüntüleyiciyle açın.

### Beklenen Çıktı

```
Pivot table exported successfully to: C:/exports/pivot.png
```

Oluşan görüntü, ekran düzeniyle aynı olacak; sütun genişlikleri, satır yükseklikleri ve uyguladığınız koşullu biçimlendirmeler dahil.

## Birden Fazla Pivot Tablosunu İşleme (İleri Düzey)

Çalışma sayfanızda birden fazla pivot tablo varsa ve sadece belirli birini istiyorsanız ne yaparsınız? `ws.getPivotTables()` üzerinden döngü yapıp isimle seçebilirsiniz:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Neden faydalıdır*: Gerçek dünyadaki raporlarda genellikle bir özet pivot ve bir detaylı pivot bulunur. İsme göre seçim, yanlışlıkla üzerine yazılmasını önler.

## Yaygın Tuzaklar ve Nasıl Önlenir

| Issue | Symptom | Fix |
|------|----------|-----|
| **Eksik çalışma sayfası** | `ws` erişilirken `IndexOutOfBoundsException` | Dizine erişmeden önce `workbook.getWorksheets().getCount() > 0` olduğundan emin olun. |
| **Pivot tablo yok** | Sessiz hata veya boş görüntü | `ws.getPivotTables().getCount()` kontrolünü kullanın (Bkz. Adım 2). |
| **Yanlış görüntü formatı** | Çıktı bulanık görünüyor veya artefaktlar var | Kayıpsız çıktı için her zaman `setImageFormat(ImageFormat.PNG)` kullanın; metin ağırlıklı tablolar için JPEG’den kaçının. |
| **Dosya yolu yazılabilir değil** | `toImage` sırasında `IOException` | Dizinin var olduğundan emin olun (`new File(outputPath).getParentFile().mkdirs()`). |

## Pro Tip: Web Uygulamaları için Bayt Dizisine Dışa Aktarın

PNG'yi doğrudan tarayıcıya döndüren bir web servisi oluşturuyorsanız, dosya yerine bir `ByteArrayOutputStream`'e yazabilirsiniz:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

Bu, geçici dosyalara ihtiyaç duyulmasını ortadan kaldırır ve yanıtı hızlandırır.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, tartışılan tüm en iyi uygulamaları içeren tam, kopyala‑yapıştır hazır program bulunmaktadır.

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Bu sınıfı çalıştırdığınızda `C:/exports` içinde `pivot.png` oluşturulur. Dosyayı açtığınızda orijinal pivot tablonun tam bir görsel kopyasını göreceksiniz—raporlara, e-postalara veya web sayfalarına yerleştirmek için mükemmel.

![PNG olarak kaydedilmiş dışa aktarılan pivot tablo – bir excel pivot görüntüsü örneği](https://example.com/images/pivot-export.png "pivot tablo örneği dışa aktar")

*Image alt text:* **PNG Excel pivot görüntüsü gösteren dışa aktarılan pivot tablo örneği**

## Sonuç

Excel'den Java kullanarak yüksek kaliteli bir PNG'ye **pivot tablosu** verisini nasıl **dışa aktaracağınızı** gösterdik. Temel adımlar: çalışma kitabını yüklemek, pivotu bulmak, `ImageOrPrintOptions`'ı **PNG formatını ayarlamak** için yapılandırmak ve sonunda `toImage`'ı çağırmak.  

Bu bilgiyle artık rapor oluşturmayı otomatikleştirebilir, pivot anlık görüntülerini panolara gömebilir veya doğrudan bir web API'sinden sunabilirsiniz. Sonraki adımda **excel pivot image** ölçeklendirme seçeneklerini keşfedebilir, su işaretleri ekleyebilir veya PNG'yi yazdırılabilir raporlar için PDF'ye dönüştürebilirsiniz.  

Büyük çalışma kitaplarıyla çalışmak veya Spring Boot ile entegrasyon hakkında sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Bu rehberde gösterilen tekniklere dayanan, yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells for Java ile Excel Pivot Tablo Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Pivot Tablo Stilini Otomatikleştirme ve Kaydetme: Kapsamlı Rehber](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Aspose.Cells Java ile Excel Pivot Tablo Manipülasyonu: Kapsamlı Rehber](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}