---
date: '2026-09-02'
description: Aspose.Cells for Java ile tıklanabilir resimli Excel çalışma kitapları
  oluşturmayı öğrenin, etkileşimli elektronik tablolar için resimlere hiperlink ekleyerek.
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: Aspose.Cells for Java ile tıklanabilir resimli Excel çalışma kitapları
  oluşturmayı öğrenin, birkaç satır kodla hiperlinkler, ekran ipuçları ekleyerek ve
  performansı optimize ederek.
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: Aspose.Cells for Java ile tıklanabilir resimli Excel oluşturun
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: Aspose.Cells for Java ile tıklanabilir resimli Excel oluşturun
url: /tr/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java ile tıklanabilir resim Excel oluşturma

## Giriş

Tek bir tıklama ile kullanıcıların web sitelerine, belgelere veya diğer kaynaklara geçmesini sağlayan **tıklanabilir resim Excel** çalışma kitapları oluşturmak istiyorsanız doğru yerdesiniz. Bu öğreticide, Aspose.Cells for Java'nın **Excel resimlerine hiperlink ekleme** nesnelerini nasıl ekleyebileceğinizi, ekran ipuçlarını nasıl yapılandırabileceğinizi ve elektronik tablolarınızı hem güzel hem de işlevsel tutabileceğinizi adım adım göstereceğiz.

### Öğrenecekleriniz
- Java'da bir Aspose.Cells çalışma kitabı başlatma.  
- Bir resim ekleme ve onu tıklanabilir bir hiperlinke dönüştürme.  
- `addHyperlink`, `setPlacement` ve `setScreenTip` gibi temel yöntemler.  
- Performans ve lisanslama için en iyi uygulamalar.

## Hızlı cevaplar
- **Gerekli kütüphane nedir?** Aspose.Cells for Java.  
- **.xlsx dosyalarını kullanabilir miyim?** Evet – API hem .xls hem .xlsx ile çalışır.  
- **Lisans gerekli mi?** Değerlendirme için bir deneme sürümü çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Kaç satır kod?** Tıklanabilir bir resim eklemek için yaklaşık 20 satır.  
- **Thread‑safe mi?** Workbook nesneleri thread‑safe değildir; her thread için ayrı örnekler oluşturun.  
- **Excel'de ekran ipucu ekleyebilir miyim?** Evet – faydalı bir üzerine gelme metni göstermek için `Hyperlink.setScreenTip()` kullanın.

## Aspose.Cells for Java ile tıklanabilir resim Excel nasıl oluşturulur

Bir `Workbook` yükleyerek veya oluşturarak, bir `Picture` nesnesi ekleyerek, bu resme bir `Hyperlink` ekleyerek, isteğe bağlı olarak bir ekran ipucu ayarlayarak ve sonunda dosyayı kaydederek tıklanabilir resim Excel çalışma kitabı oluşturursunuz. API, tüm düşük seviyeli Excel XML'lerini yönetir, böylece sadece birkaç basit Java satırı yazmanız yeterlidir.

### Önkoşullar
Başlamadan önce şunların olduğundan emin olun:

- **Aspose.Cells for Java** (v25.3 veya daha yeni).  
- **JDK 8+** yüklü.  
- Bir IDE (IntelliJ IDEA, Eclipse veya NetBeans) ve bağımlılık yönetimi için Maven veya Gradle.

### Gerekli kütüphaneler
Aspose.Cells'i projenize ekleyin:

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

### Lisans edinme
Aspose.Cells ticari bir üründür, ancak ücretsiz bir deneme sürümüyle başlayabilir veya geçici bir lisans talep edebilirsiniz:

- Ücretsiz deneme: [Aspose Downloads](https://releases.aspose.com/cells/java/) adresinden indirin.  
- Geçici lisans: [Temporary License page](https://purchase.aspose.com/temporary-license/) üzerinden talep edin.  
- Satın alma: Uzun vadeli kullanım için [Aspose Purchase](https://purchase.aspose.com/buy) adresini ziyaret edin.

### Temel başlatma
`Workbook` sınıfı, bellekteki bir Excel dosyasının tamamını temsil eder. Bu sınıfı örnekleyip ardından ilk çalışma sayfasına bir referans alırsınız. `Worksheet` ise çalışma kitabı içindeki tek bir sayfayı temsil eder.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

## Adım adım uygulama

### Adım 1: çalışma kitabınızı hazırlayın
Yeni bir çalışma kitabı oluşturarak ve ilk sayfayı seçerek başlarız.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```  

### Adım 2: bir etiket ekleyin ve hücre boyutunu ayarlayın
Açıklayıcı bir etiket ekleyin ve hücreye resim için yeterli alan sağlayın.

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### Adım 3: resmi ekleyin
`Picture` bir çalışma sayfasına yerleştirilen resim nesnesini temsil eder.

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*İpucu*: `"path/to/aspose-logo.jpg"` ifadesini gerçek resim dosyanızın yolu ile değiştirin.

### Adım 4: konumu yapılandırın ve hiperlinki ekleyin
`Hyperlink` bir hücre, şekil veya resim ile ilişkili bir bağlantıyı tanımlar ve tıklandığında gezinmeyi sağlar.

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### Adım 5: bir ekran ipucu ayarlayın ve çalışma kitabını kaydedin
Yararlı bir araç ipucu sağlayın ve çalışma kitabını diske yazın.

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## Neden Excel resmine hiperlink eklenir?

Tıklanabilir bir resim gömmek, marka öğelerini, simgeleri veya diyagramları doğrudan gezinme noktalarına dönüştürmenizi sağlar ve ilgili içeriğe ulaşmak için gereken tıklama sayısını azaltır. Bu yaklaşım, pazarlama panoları, teknik kılavuzlar ve eğitim çalışma sayfalarında kullanıcı verimliliğini artırır.

## Excel'e ekran ipucu nasıl eklenir

Resme eklenmiş `Hyperlink` nesnesi üzerinde `hyperlink.setScreenTip("Your tip here")` çağrısı yaparak bir ekran ipucu ekleyebilirsiniz. İpucu, imleç resmin üzerine geldiğinde görünür ve kullanıcıya sayfayı karıştırmadan bağlamsal rehberlik sağlar.

## Sorun giderme ipuçları
- **Resim yolu hataları** – dosya konumunu iki kez kontrol edin ve uygulamanın okuma izinlerine sahip olduğundan emin olun.  
- **Lisans uygulanmadı** – deneme süresi dolarsa, hiperlinkler çalışmayabilir; `License.setLicense` ile geçerli bir lisans uygulayın.  
- **Hiperlink tıklanabilir değil** – resmin `PlacementType` değerinin `FREE_FLOATING` olduğundan emin olun.

## Pratik uygulamalar
Tıklanabilir resim gömmek birçok senaryoda faydalıdır:

1. **Pazarlama raporları** – marka logolarını ürün sayfalarına bağlayın.  
2. **Teknik dokümantasyon** – ayrıntılı şemaları açan diyagramları ekleyin.  
3. **Eğitim çalışma sayfaları** – simgeleri ek video kısayollarına dönüştürün.  
4. **Proje panoları** – durum simgelerini ilgili görev izleyicileriyle açın.

## Performans değerlendirmeleri
- Resim dosyası boyutlarını makul tutun; büyük resimler çalışma kitabı bellek kullanımını artırır.  
- Bir döngüde birçok dosya işlenirken kullanılmayan nesneleri (`workbook.dispose()`) serbest bırakın.  
- Performans iyileştirmeleri ve hata düzeltmeleri için en son Aspose.Cells sürümüne yükseltin.

## Sonuç
Artık Aspose.Cells for Java kullanarak Excel'deki resimlere nasıl hiperlink ekleyeceğinizi biliyorsunuz; bu sayede **tıklanabilir resim Excel** çalışma kitapları oluşturabilir ve bunları daha zengin ve etkileşimli hâle getirebilirsiniz. Raporlama ihtiyaçlarınıza uygun farklı URL'ler, ekran ipuçları ve resim konumlarıyla deneyler yapın. Sonraki adımda şekillere hiperlink eklemeyi veya birden çok çalışma sayfasına toplu resim eklemeyi otomatikleştirmeyi keşfedebilirsiniz.

## Sıkça sorulan sorular

**Q:** Aspose.Cells for Java tarafından desteklenen maksimum resim boyutu nedir?  
**A:** Katı bir limit yoktur, ancak çok büyük resimler performansı etkileyebilir ve dosya boyutunu artırabilir.

**Q:** Bu özelliği .xlsx dosyalarıyla kullanabilir miyim?  
**A:** Evet, API hem `.xls` hem `.xlsx` formatlarıyla çalışır.

**Q:** Hiperlink eklerken istisnaları nasıl ele almalı?  
**A:** Kodu bir try‑catch bloğuna sarın ve `Exception` ayrıntılarını kaydederek yol veya lisans sorunlarını teşhis edin.

**Q:** Bir resme eklenen hiperlinki kaldırmak mümkün mü?  
**A:** Evet – `Picture` nesnesini alın ve `pic.getHyperlink().remove()` çağırın veya resmi koleksiyondan silin.

**Q:** Hiperlinkimin beklenildiği gibi çalışmamasının nedeni ne olabilir?  
**A:** Yaygın nedenler arasında hatalı URL dizesi, eksik `http://`/`https://` ön eki veya belirli özellikleri devre dışı bırakan lisanssız bir deneme sürümü bulunur.

## Ek kaynaklar
- **Dokümantasyon:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **İndirme:** [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **Satın alma ve deneme:** Lisans seçenekleri için [Aspose Purchase](https://purchase.aspose.com/buy) veya [Temporary License Page](https://purchase.aspose.com/temporary-license/) adresini ziyaret edin.  
- **Destek forumu:** Yardım için [Aspose Support Forum](https://forum.aspose.com/c/cells/9).

---

**Son güncelleme:** 2026-09-02  
**Test edildi:** Aspose.Cells for Java 25.3  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Excel'de Aspose.Cells for Java Kullanarak Hiperlink Oluşturma - Adım Adım Kılavuz](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [Aspose.Cells for Java Kullanarak Excel Hücrelerini Stilize Etme ve Hiperlink Ekleme](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Yorumuna Resim Ekleme: Tam Kılavuz](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}