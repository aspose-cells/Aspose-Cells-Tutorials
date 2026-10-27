---
category: general
date: 2026-07-16
description: Aspose.Cells for Java kullanarak yeni bir çalışma kitabı oluşturun ve
  pivot tabloyu kopyalayın. Pivot tabloyu nasıl çoğaltacağınızı ve Excel aralığını
  dakikalar içinde nasıl kopyalayacağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: tr
lastmod: 2026-07-16
og_description: Aspose.Cells for Java ile yeni bir çalışma kitabı oluşturun ve pivot
  tabloyu kopyalayın. Bu kılavuz, pivot tabloyu nasıl çoğaltacağınızı ve Excel aralığını
  verimli bir şekilde nasıl kopyalayacağınızı gösterir.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Java'da Yeni Çalışma Kitabı Oluşturma ve Pivot Tablo Kopyalama – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Java’da Yeni Çalışma Kitabı Oluşturma ve Pivot Tabloyu Kopyalama – Tam Adım
  Adım Rehber
url: /tr/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Yeni Çalışma Kitabı Oluşturma ve Pivot Tablosunu Kopyalama – Tam Adım‑Adım Kılavuz

Hiç **create new workbook** işlemini mevcut bir dosyadan karmaşık bir pivot tabloyu koruyarak nasıl yapacağınızı merak ettiniz mi? Excel sayfasına baktığınızda “Bu pivotu başka bir çalışma kitabına ihtiyacım var” diye düşündünüz ve başınızı kaşıdıysanız, yalnız değilsiniz. İyi haber, Aspose.Cells for Java ile sadece birkaç satır kodla bir pivot tabloyu çoğaltabilirsiniz.

Bu öğreticide **copy pivot table** verilerini, **duplicate pivot table** yapılarını ve **copy Excel range** içeriklerini adım adım inceleyeceğiz—tüm bunları sıfırdan yeni bir çalışma kitabı oluştururken yapacağız. Sonunda tam olarak istediğinizi yapan çalıştırılabilir bir Java programına sahip olacaksınız.

## Öğrenecekleriniz

- Aspose.Cells ile programlı olarak **create new workbook** nasıl yapılır.
- Pivot tabloyu içeren aralığı tanımlamanın kesin yolu.
- **copy pivot table** ve **duplicate pivot table** işlemlerini biçimlendirme veya veri bağlantılarını kaybetmeden nasıl yapacağınız.
- **copy Excel range** verimli bir şekilde nasıl kopyalanır ve sonuç nasıl kaydedilir.
- Büyük pivot tablolarla çalışırken yaygın tuzaklar ve ipuçları.

Harici referanslara gerek yok—her şey kendi içinde, çalıştırılabilir ve açıklamalı.

## Önkoşullar

1. **Java Development Kit (JDK) 11+** – herhangi bir yeni sürüm çalışır.
2. **Aspose.Cells for Java** kütüphanesi (2026‑07‑16 tarihindeki en son sürüm). Maven Central'dan edinebilirsiniz:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Pivot tablo içeren bir kaynak Excel dosyası (`SourceWithPivot.xlsx`).
4. Bir IDE veya basit metin editörü—IntelliJ IDEA, Eclipse veya VS Code yeterli.

Hepsine sahip misiniz? Harika—başlayalım.

## Adım 1: **Create New Workbook** ve Kaynak Dosyayı Yükleme

İlk olarak, çoğaltılmış pivotu tutacak yeni bir çalışma kitabı nesnesine ihtiyacımız var. Aynı zamanda, pivot tablo aralığını referans alabilmek için orijinal çalışma kitabını da yüklemeliyiz.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Neden önemli:**  
> Kaynak çalışma kitabını yüklemek, pivotu kapsayan temel `Range` nesnesine erişim sağlar. Bu adımı atlayarsanız kopyalanacak bir şey olmaz ve **duplicate pivot table** işlemi sessizce başarısız olur.

## Adım 2: Pivotu İçeren **Copy Excel Range** Tanımlama

Bir pivot tablo tek bir hücre değildir—dikdörtgen bir blok olarak yayılır. Aspose.Cells'e hangi hücrelerin kopyalanacağını tam olarak söylememiz gerekir.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **İpucu:**  
> Tam aralıktan emin değilseniz, kaynak çalışma kitabını Excel'de açın, pivotu seçin ve ad kutusuna bakın. `A1:G20` gibi bir şey gösterir. Tam aralığı kullanmak, daha sonra **copy pivot table** yaptığımızda tüm alan ayarları, filtreler ve hesaplamaların korunmasını sağlar.

## Adım 3: Kopyalanan Pivotu Alacak **Create New Workbook**

Şimdi yepyeni bir çalışma kitabı oluşturuyoruz—burada **duplicate pivot table** yer alacak.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Arka planda ne oluyor?**  
> Varsayılan yapıcı, tek bir boş sayfa içeren bir çalışma kitabı oluşturur. Bu, **create new workbook** senaryosu için ihtiyacımız olan temiz bir tuvaldir. Kalan stil veya gizli sayfalardan endişe etmenize gerek yok.

## Adım 4: **Copy Pivot Table** – Tanımlanan Excel Aralığını Gerçekten Kopyala

Kaynak ve hedef hazır olduğunda, kopyalama işlemini gerçekleştiririz. Bu adım, bulmacanın **how to copy pivot** kısmını tamamlar.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Neden `copy` pivotlar için çalışır:**  
> Aspose.Cells, pivotu hücre koleksiyonunun bir parçası olarak ele alır. Aralığı kopyaladığınızda pivot önbelleği, alan listesi ve düzeni de taşır. Sonuç, yeni çalışma kitabında tam işlevsel bir **duplicate pivot table** olur.

## Adım 5: Sonucu Kaydet ve **Copy Pivot Table** İşlemini Doğrula

Son olarak, hedef çalışma kitabını diske kaydedin. Excel'de dosyayı açarak pivotun kaynakta olduğu gibi göründüğünden emin olun.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Beklenen sonuç:**  
- `CopyPivotResult.xlsx` dosyası, `SourceWithPivot.xlsx` içinde gördüğünüz aynı pivot tabloyu içeren bir çalışma sayfası ile açılır.  
- Tüm satır/sütun etiketleri, filtreler ve hesaplanmış alanlar korunur.  
- Artık kaynak veriyi bağımsız olarak düzenleyebilir ve yeni çalışma kitabı kendi pivot önbelleğini tutar.

## Kenar Durumları ve Yaygın Sorular

### Kaynak pivot birden fazla sayfaya yayılmışsa ne olur?

Aspose.Cells aynı anda yalnızca tek bir çalışma sayfası içinde aralıkları kopyalayabilir. Pivotunuz birden fazla sayfaya yayılmışsa, ilgili her aralığı ayrı ayrı kopyalamanız ve ardından manuel olarak yeniden bağlamanız gerekir.

### Bu yöntem özel sayı formatlarını korur mu?

Evet. `copy` yöntemi hücre stillerini, sayı formatlarını, yazı tiplerini ve renkleri kopyalar. Ancak, dış aralıkları referans alan koşullu biçimlendirmeleriniz varsa, kopyalama sonrası bu referansları iki kez kontrol edin.

### Dış veri kaynağı kullanan bir pivotu nasıl kopyalarsınız?

Pivot dış bir bağlantıdan (ör. bir SQL sorgusu) veri çekiyorsa, bağlantı bilgileri `copy` ile **aktarılmaz**. Hedef çalışma kitabında veri kaynağını yeniden oluşturmanız veya önceden kaynak veriyi gömmeniz gerekir.

### Alt veri olmadan sadece pivot düzenini kopyalayabilir miyim?

Bunu, önce kaynak aralıktaki veri hücrelerini temizleyip ardından sadece pivotun düzenini kopyalayarak yapabilirsiniz. Bu daha gelişmiş bir senaryodur ve genellikle basit bir **duplicate pivot table** görevi için gerekli değildir.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda eksiksiz, çalıştırılmaya hazır Java sınıfı bulunmaktadır. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek klasör yolu ile değiştirin.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Programı çalıştırın (`java CopyPivotTableDemo`) ve başarı mesajını konsolda göreceksiniz.

## Profesyonel İpuçları ve En İyi Uygulamalar

- **Validate the range** kopyalamadan önce doğrulayın. `"A1:G20"` gibi sabit bir değer kodlamak istemiyorsanız, kullanılan alanı programatik olarak keşfetmek için `srcWs.getCells().maxDisplayRange` kullanın.
- **Turn off calculation** büyük çalışma kitapları için kopyalamayı hızlandırmak amacıyla geçici olarak devre dışı bırakın:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) uzun süren hizmetlerde bellek sızıntılarını önlemek için.
- **Version compatibility:** Kod, Aspose.Cells 23.12 ve sonrası ile çalışır. Daha eski sürümler `copy` yerine `srcRange.copyTo` gerektirebilir.

## Sonraki Adımlar

Artık **create new workbook** ve **copy pivot table** konularında uzmanlaştığınıza göre, şunları keşfedebilirsiniz:

- **How to copy pivot** bir toplu işte birden fazla çalışma sayfasına kopyalama.
- Pivotun yanında düzenli veri tabloları için **copy excel range** ekleme.
- Bir döngü kullanarak her ayın raporu için **duplicate pivot table** oluşturmayı otomatikleştirme.
- Kopyalanan pivotu Aspose.Cells’ın yerleşik renderları ile PDF veya HTML olarak dışa aktarma.

## Sonuç

Aspose.Cells kullanarak Java'da **create new workbook**, kaynak **copy excel range** tanımlama ve **copy pivot table** ile **duplicate pivot table** oluşturma sürecini adım adım inceledik. Çözüm kısa, tamamen işlevsel ve üretim kullanımına hazır. Aralığı değiştirmek, farklı kaynak dosyalarla denemek veya bu mantığı daha büyük bir raporlama hattına entegre etmekten çekinmeyin.

Herhangi bir sorunla karşılaşırsanız veya bu öğreticiyi genişletmek için fikirleriniz varsa, aşağıya yorum bırakın. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}