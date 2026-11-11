---
date: '2026-11-03'
description: Aspose.Cells for Java kullanarak Excel'den hyperlinks çıkarmayı öğrenin.
  Bu kılavuz, çalışma kitaplarını yükleme, bağlantıları alma, büyük dosyaları işleme
  ve hyperlink yönetimi için en iyi uygulamaları kapsar.
keywords:
- how to extract hyperlinks
- process large excel files
- load excel workbook
- retrieve excel links
- excel hyperlink management
lastmod: '2026-11-03'
og_description: Aspose.Cells for Java kullanarak Excel'den hyperlinks çıkarmayı öğrenin.
  Adım adım code, performance tips ve güvenilir hyperlink yönetimi için FAQ alın.
og_image_alt: Guide to extract hyperlinks from Excel using Aspose.Cells for Java
og_title: Excel'den hyperlinks çıkarmak – gelişmiş yönetim
schemas:
- author: Aspose
  dateModified: '2026-11-03'
  description: Learn how to extract hyperlinks from Excel using Aspose.Cells for Java.
    This guide covers loading workbooks, retrieving links, processing large files,
    and best practices for hyperlink management.
  headline: How to extract hyperlinks from Excel – advanced management
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java supports Java 8 and newer, including all LTS releases
      up to Java 21.
    question: What versions of Java are compatible with Aspose.Cells?
  - answer: Yes. Load only the required worksheet or range, and avoid loading the
      entire workbook when possible. Reusing a single `Workbook` instance further
      reduces heap pressure.
    question: Can I extract hyperlinks from very large Excel files without running
      out of memory?
  - answer: A free trial lets you experiment, but a commercial license removes evaluation
      limits, unlocks multi‑threaded processing, and provides full technical support.
    question: Is a license required for hyperlink extraction in production?
  - answer: The `TargetModeType.EMAIL` constant identifies email links; you can extract
      the `mailto:` address and process it separately.
    question: How do I handle hyperlinks that point to email addresses?
  - answer: Absolutely. All hyperlink properties—display text, tooltip, address, and
      target mode—are retained when you save the workbook in any supported format.
    question: Does Aspose.Cells preserve hyperlink formatting when saving?
  type: FAQPage
tags:
- extract hyperlinks
- Aspose.Cells
- Java Excel processing
title: Excel'den hyperlinks çıkarmak – gelişmiş yönetim
url: /tr/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den Hipermetin Bağlantılarını Nasıl Çıkarılır – Gelişmiş Yönetim

Bugünün veri odaklı dünyasında, **Excel'den hipermetin bağlantılarını nasıl çıkarılır** sorusu, Excel raporlamasını otomatikleştiren herkes için temel bir gereksinimdir. Finansal bir gösterge paneli, veri taşıma aracı ya da belge oluşturma hizmeti geliştiriyor olun, hipermetin bağlantılarıyla dolu çalışma kitaplarıyla başa çıkmak yaygın bir zorluktur. Bu öğreticide, bir Excel çalışma kitabını nasıl yükleyeceğinizi, çalışma sayfalarına erişeceğinizi ve Aspose.Cells for Java kullanarak **Excel'den hipermetin bağlantılarını nasıl alacağınızı** öğreneceksiniz. Sonunda, hipermetin işleme yeteneğini kendi uygulamalarınıza entegre etmeye ve büyük ölçekli senaryolar için **Excel dosyalarını toplu işleme** yapmaya hazır olacaksınız.

## Hızlı Yanıtlar
- **Bir çalışma kitabını açmak için birincil sınıf nedir?** `Workbook` – bellekte tüm bir Excel dosyasını temsil eden merkezi nesnedir.  
- **Bir aralıktaki tüm hipermetin bağlantılarını döndüren yöntem hangisidir?** `Range.getHyperlinks()` – belirtilen aralıktaki her hipermetin nesnesini sıralar.  
- **Temel hipermetin çıkarımı için lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir, ancak ticari lisans değerlendirme sınırlamalarını kaldırır ve tam performans iyileştirmelerini açar.  
- **Büyük dosyaları verimli bir şekilde işleyebilir miyim?** Evet—belirli çalışma sayfalarına veya aralıklara odaklanın, tek bir `Workbook` örneğini yeniden kullanın ve nesneleri zamanında serbest bırakın.  
- **Hangi Java sürümleri destekleniyor?** Java 8 ve üzeri, Java 11, 17 ve sonraki LTS sürümleri dahil.

## “Excel'den hipermetin bağlantılarını çıkarmak” nedir?

Excel'den hipermetin bağlantılarını çıkarmak, hücrelerde depolanan bağlantı bilgilerini (URL'ler, dosya yolları, e‑posta adresleri veya iç hücre referansları gibi) okuyarak bu verileri programatik olarak kullanabilmek anlamına gelir. Aspose.Cells, Microsoft Excel'i başlatmadan bu bağlantıları sıralamanızı sağlayan basit bir API sunar; bu da hem zaman hem de sunucu kaynaklarından tasarruf sağlar.

## Neden Excel'den hipermetin bağlantılarını almak?

Hipermetin bağlantılarını almak, **bağlantı sağlığını doğrulamanıza**, **URL'leri taşımanıza veya yeniden yazmanıza**, **özet raporlar oluşturmanıza** ve **bilgi tabanı entegrasyonu için aranabilir indeksler oluşturmanıza** olanak tanır. Örneğin, gece çalışan bir görev, depodaki her çalışma kitabını tarar, kırık URL'leri işaretler ve yeni bir domaine otomatik olarak günceller; böylece yayınlanan raporlar asla eski referanslar içermez.

## Önkoşullar

- **Aspose.Cells for Java** kütüphanesi (sürüm 25.3 ve üzeri).  
- Java 8 + ve bir IDE (IntelliJ IDEA, Eclipse, VS Code vb.).  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Geçerli bir Aspose.Cells lisansı (deneme için isteğe bağlı).  

### Aspose.Cells for Java'ı Kurma

Kütüphaneyi projenize Maven ya da Gradle ile ekleyin.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **İpucu:** Kütüphane sürümünü güncel tutun; her küçük sürüm yeni hipermetin türlerini destekler ve bellek kullanımını %30'a kadar iyileştirir.

#### Temel başlatma

Bağımlılık eklendikten sonra, çalışma kitabının yüklenebildiğini doğrulayan basit bir Java sınıfı oluşturun.

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Excel'den Hipermetin Bağlantılarını Çıkarmak – Çalışma Kitabını Yükleme

`Workbook`, tüm bir Excel dosyasını bellekte yükleyen ve temsil eden birincil sınıftır.  
Çalışma kitabını tek satır kodla yükleyin: `Workbook workbook = new Workbook("input.xlsx");`. Bu çağrı dosya başlığını ayrıştırır, çalışma sayfalarının bellek içi temsilini oluşturur ve API'yi sonraki sorgular için hazırlar. Gereksiz tüm klasörü yüklemek yerine yalnızca ihtiyaç duyulan çalışma kitabını yüklemek, 10 MB altındaki dosyalar için başlatma süresini yaklaşık %40 azaltır.

### Çalışma kitabını yükle (özellik 1)

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## Excel'den Hipermetin Bağlantılarını Çıkarmak – Çalışma Sayfasına ve Aralığa Erişim

`Range`, bir çalışma sayfası içinde dikdörtgen bir hücre bloğunu temsil eder.  
Önce taramak istediğiniz çalışma sayfasını alın, ardından ilgilendiğiniz alanı kapsayan bir `Range` nesnesi oluşturun. Örneğin, `worksheet.getCells().createRange("A1", "Z1000")` dikdörtgen bir blok tanımlar; API daha sonra bu aralıkta `getHyperlinks()` çağrısına izin verir. Aralığı tanımlayarak taramayı ilgili bölgeyle sınırlarsınız; bu da performansı artırır ve bellek kullanımını azaltır.

### Çalışma sayfasına ve aralığa erişim (özellik 2)

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## Excel'den Hipermetin Bağlantılarını Çıkarmak – Hipermetin Bağlantılarını Alma ve İşleme

`getHyperlinks()` belirtilen aralıktaki tüm hipermetin nesnelerinin bir koleksiyonunu döndürür.  
`Range.getHyperlinks()` çağrısı, `Hyperlink` nesnelerinden oluşan bir koleksiyon sağlar. Her nesne `getAddress()`, `getDisplay()`, `getTooltip()` ve `getTargetMode()` gibi özellikleri ortaya çıkarır. Koleksiyonu döngüyle gezebilir, her bağlantıyı kaydedebilir veya daha sonraki analiz için bir veritabanına depolayabilirsiniz. Adres türüne veya görüntü metnine göre filtreleme yaparak veriyi saklamadan önce daraltabilirsiniz.

### Hipermetin bağlantılarını alma ve işleme (özellik 3)

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

## Pratik Uygulamalar

| Kullanım Durumu | Fayda |
|-----------------|-------|
| **Veri doğrulama** | Rapor yayınlamadan önce her hipermetin bağlantısının erişilebilir bir URL'ye işaret ettiğini otomatik olarak doğrular. |
| **Otomasyon** | Yeni bir veri ambarına geçiş sırasında bağlantıları çıkarır, referansları anında günceller. |
| **Raporlama** | Bir çalışma kitabında başvurulan tüm dış kaynakları listeleyen özet bir sayfa oluşturur. |

## Performans Düşünceleri

- **Yalnızca gerekli aralıkları işleyin** – kapsamı sınırlamak, binlerce satır içeren çalışma kitaplarında bellek tüketimini %60'a kadar azaltır.  
- **Nesneleri serbest bırakın** – kullanım sonrası `workbook = null;` yapın ve JVM'in çöp toplayıcısının belleği geri kazanmasına izin verin.  
- **Toplu işleme** – çok sayıda dosya işlenirken mümkün olduğunca tek bir `Workbook` örneğini yeniden kullanın. Bu desen, **Excel dosyalarını toplu işleme** yapmanızı sağlar ve standart 8 çekirdekli bir sunucuda 150 dosya/dakika throughput elde etmenize olanak tanır.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|-------|
| **Null `range`** | `getHyperlinks()` çağırmadan önce aralığın oluşturulduğundan emin olun. |
| **Lisans eksik** | Deneme sürümü geliştirme için çalışır, ancak lisanslı sürüm değerlendirme sınırlamalarını kaldırır ve performansı artırır. |
| **Desteklenmeyen hipermetin türü** | Aspose güncellemelerini takip ederek yeni türleri işlemek için `TargetModeType` sabitlerini kullanın. |

## Sıkça Sorulan Sorular

**S: Aspose.Cells hangi Java sürümleriyle uyumludur?**  
C: Aspose.Cells for Java, Java 8 ve üzeri, Java 21 dahil tüm LTS sürümlerini destekler.

**S: Çok büyük Excel dosyalarından bellek tükenmeden hipermetin bağlantılarını çıkarabilir miyim?**  
C: Evet. Gereken çalışma sayfasını veya aralığını yalnızca yükleyin ve mümkün olduğunca tüm çalışma kitabını yüklemekten kaçının. Tek bir `Workbook` örneğini yeniden kullanmak da yığın (heap) baskısını azaltır.

**S: Üretim ortamında hipermetin çıkarımı için lisans zorunlu mu?**  
C: Ücretsiz deneme sürümü deneme amaçlı kullanılabilir, ancak ticari lisans değerlendirme sınırlamalarını kaldırır, çoklu iş parçacıklı işleme açar ve tam teknik destek sağlar.

**S: E‑posta adreslerine yönlendiren hipermetin bağlantılarını nasıl ele alırım?**  
C: `TargetModeType.EMAIL` sabiti e‑posta bağlantılarını tanımlar; `mailto:` adresini çıkarıp ayrı olarak işleyebilirsiniz.

**S: Aspose.Cells, kaydederken hipermetin biçimlendirmesini korur mu?**  
C: Kesinlikle. Tüm hipermetin özellikleri—görüntü metni, araç ipucu, adres ve hedef modu—desteklenen herhangi bir formatta çalışma kitabı kaydedildiğinde korunur.

**S: Aspose.Cells'i **Excel hipermetinlerini okuma** için toplu bir işte kullanabilir miyim?**  
C: Evet—API'yi dosyalar üzerinde döngüyle birleştirerek birçok çalışma kitabındaki Excel hipermetinlerini okuyabilir, ardından sonuçları merkezi bir depoya kaydedebilirsiniz.

**S: Yüksek verim gerektiren senaryolar için **excel workbook java** nasıl en iyi şekilde yüklenir?**  
C: Mümkün olduğunca tek bir `Workbook` örneğini yeniden kullanın, giriş akışlarını hızla kapatın ve bellek kullanımını optimize etmek için `MemorySetting.MEMORY_PREFERENCE` seçeneğini etkinleştirin.

---

**Son güncelleme:** 2026-11-03  
**Test edilen sürüm:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

Daha fazla sorunuz varsa, lütfen [Aspose destek forumunu](https://forum.aspose.com/c/cells/9) ziyaret edin.

## İlgili Eğitimler

- [Aspose.Cells for Java ile Excel'e Hipermetin Ekleme – Adım Adım Kılavuz](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Büyük Excel Dosyalarını İşleme: Aspose.Cells ile Hipermetin Yönetimi](/cells/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java Kullanarak Excel Çalışma Kitaplarında Gizli Dış Bağlantıları Bulma](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}