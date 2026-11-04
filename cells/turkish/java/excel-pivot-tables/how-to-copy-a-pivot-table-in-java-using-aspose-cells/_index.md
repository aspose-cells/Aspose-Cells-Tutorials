---
category: general
date: 2026-09-27
description: Aspose.Cells ile Java’da pivot tablo kopyalama – aralığı nasıl kopyalayacağınızı
  ve pivot tanımlarını nasıl koruyacağınızı gösteren adım adım bir rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: tr
lastmod: 2026-09-27
og_description: Aspose.Cells kullanarak Java'da özet tabloyu kopyalayın. Özet tablo
  tanımlarını bozmadan aralığı kopyalamak için bu kapsamlı öğreticiyi izleyin.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Java'da bir pivot tablo kopyalama – Aspose.Cells hızlı rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java'da Aspose.Cells kullanarak bir pivot tabloyu nasıl kopyalarız
url: /tr/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells Kullanarak Pivot Tablosunu Kopyalama

Bir çalışma kitabından diğerine **copy pivot table** yapmanız gerekiyorsa, bu kılavuz Aspose.Cells for Java ile bunu tam olarak nasıl yapacağınızı gösterir. Çözüm, oluşturduğunuz herhangi bir pivot için çalışır ve pivot tanımını manuel yeniden oluşturma olmadan korur.

Kaynak dosyayı nasıl yükleyeceğinizi, pivotun bulunduğu aralığı nasıl tanımlayacağınızı, bu aralığı yeni bir çalışma kitabına nasıl kopyalayacağınızı ve sonunda sonucu nasıl kaydedeceğinizi öğreneceksiniz. Eğitim ayrıca veri kaynaklarını koruma ve büyük çalışma kitaplarıyla başa çıkma gibi yaygın tuzakları da kapsar.

## İhtiyacınız Olanlar

* Java 17 veya daha yeni (kod JDK 8+ ile de derlenir)
* Aspose.Cells for Java 23.9 veya daha yeni – en son sürüm, en güvenilir **copy range aspose cells** desteğini sunar
* Pivot tablo içeren bir kaynak Excel dosyası (ör. `SourceWithPivot.xlsx`)
* Aspose.Cells JAR'ını referans alabilen bir IDE veya yapı aracı (Maven/Gradle)

## Adım 1: Pivot tabloyu içeren kaynak çalışma kitabını yükleyin

İlk adım, kopyalamak istediğiniz pivotu içeren çalışma kitabını açmaktır. Dosyayı yüklemek, tüm çalışma sayfalarının, hücrelerin ve pivot önbelleklerinin bellek içi bir temsilini oluşturur.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Neden Bu Önemli:**  
Aspose.Cells, gizli pivot önbellek sayfaları dahil tüm çalışma kitabını okur. Bu adımı atlayarsanız, sonraki **copy pivot table** işlemi temel veri kaynağını kaybeder.

## Adım 2: Boş bir hedef çalışma kitabı oluşturun

Sonra, kopyalanan pivotu alacak yeni bir çalışma kitabı örneği oluşturun. Temiz bir çalışma kitabıyla başlamak, yanlışlıkla üzerine yazılmasını önler.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**İpucu:**  
Varsayılan çalışma kitabı bir boş sayfa içerir; bu basit bir kopyalama için mükemmeldir. Belirli bir sayfa adına kopyalamanız gerekiyorsa, `destWs`'i `destWs.setName("TargetSheet")` ile yeniden adlandırın.

## Adım 3: Pivot tabloyu içeren kaynak aralığını tanımlayın

Bir pivot tablo, hücrelerin dikdörtgen bir bloğunu kaplar. Tam aralığı belirtmeniz gerekir; aksi takdirde yalnızca ham veri kopyalanır. Bu örnekte pivotun **A1:G20** aralığını kapladığını varsayıyoruz, ancak dosyanıza uygun şekilde adresi ayarlayabilirsiniz.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Neden Bu Çalışıyor:**  
`createRange` metodunu çalışma sayfasının `Cells` koleksiyonunda çağırdığınızda, Aspose.Cells pivot tanımını, önbelleğini ve tüm biçimlendirmeleri içerir. Bu, **how to copy pivot table** işleminin doğru şekilde yapılmasının temelidir.

## Adım 4: Tanımlanan aralığı hedef sayfaya kopyalayın

Şimdi `copy` metodunu kullanarak aralığı çoğaltın. Metod, aralık içindeki her şeyi, pivot tanımını, formülleri ve stilleri kopyalar.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Önemli Not:**  
Sadece pivot olmadan veriye ihtiyacınız varsa, `srcRange.copyData` kullanabilirsiniz. Ancak gerçek bir **copy pivot table** için yukarıda gösterildiği gibi tüm aralığı kopyalamanız gerekir.

## Adım 5: Hedef çalışma kitabını kaydedin

Son olarak, yeni çalışma kitabını diske yazın. Oluşan dosya, kaynakla aynı tam işlevsel pivot tabloyu içerecektir.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Programı çalıştırmak, orijinal dosyayla aynı pivot düzeni, filtreler ve hesaplamalara sahip `CopyPivotResult.xlsx` dosyasını üretir.

## Beklenen Çıktı

Excel'de `CopyPivotResult.xlsx` dosyasını açtığınızda:

* Pivot tablo, ilk sayfada **A1:G20** aralığında görünür.
* Tüm satır/sütun alanları, filtreler ve değer alanları korunur.
* Pivotu yenilemek, kaynak çalışma kitabıyla aynı veri kaynağını günceller (kaynak veri gömülü ise).

## Kenar Durumları ve Pratik İpuçları

| Durum | Nasıl Ele Alınır |
|-----------|------------------|
| **Pivot beklenenden daha fazla sütun kapsıyor** | Programmatically tam adresi elde etmek için `srcWs.getPivotTables().get(0).getPivotTableArea()` kullanın. |
| **Kaynak çalışma kitabı birden fazla pivot içeriyor** | Her bir aralığı ayrı ayrı kopyalamak ve hedef adresleri ayarlamak için `srcWs.getPivotTables()` üzerinden döngü oluşturun. |
| **Büyük çalışma kitapları bellek baskısına neden olur** | Kaynağı yüklemeden önce `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` etkinleştirin. |
| **Sadece pivot tanımını, veriyi değil, kopyalamanız gerekiyor** | Kopyaladıktan sonra, hedefteki kaynak veri satırlarını `destWs.getCells().deleteRows(startRow, count)` ile silin. |
| **Hedef dosya orijinal biçimlendirmeyi korumalı** | Tam bir doğruluk kopyası için `CopyOptions`'ı `options.setPasteType(PasteType.ALL)` olarak ayarlayın. |

**Pro ipucu:** Kopyalanan pivotu her zaman `destWs.getPivotTables().get(0).refresh()` metodunu programmatically çağırarak doğrulayın. Bu, özellikle kaynak veri harici bir bağlantıda bulunduğunda önbelleğin güncel olmasını sağlar.

## Tam Çalıştırılabilir Örnek

Aşağıda IDE'nize kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirin.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Bu kodu çalıştırmak, **copy pivot table** işlemini tam olarak açıklandığı gibi gerçekleştirecek ve pivot işlevselliğini korurken **copy range aspose cells**'i en basit şekilde nasıl yapacağınızı gösterir.

## Sonuç

Artık Aspose.Cells kullanarak Java'da **copy pivot table** işlemini, kaynak çalışma kitabını yüklemekten hedef dosyayı kaydetmeye kadar biliyorsunuz. Kılavuz temel adımları kapsadı, her adımın neden önemli olduğunu açıkladı ve yaygın kenar durumlarını ele aldı.

Sonraki adımda şunları keşfedebilirsiniz:

* **how to copy pivot table** aynı çalışma kitabı içinde farklı çalışma sayfalarına
* **copy range aspose cells** kullanarak grafikleri veya koşullu biçimlendirmeyi çoğaltma
* Kopyalama sonrası veriyi güncel tutmak için pivot yenilemeyi otomatikleştirme

Daha büyük aralıklarla, birden fazla pivotla veya bu mantığı daha büyük bir Excel işleme hattına entegre ederek denemeler yapmaktan çekinmeyin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Java'da Pivot Tablosunu Kopyala – Koruyun, PPTX'e Aktarın](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Aspose.Cells for Java ile Excel Pivot Tablo Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells Java ile Excel Pivot Tablo Manipülasyonu: Kapsamlı Rehber](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}