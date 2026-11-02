---
date: '2026-04-05'
description: Aspose.Cells ile Java’da grafik oluşturmayı, Excel grafiğini görüntüye
  dönüştürmeyi ve grafiği verimli bir şekilde dışa aktarmayı öğrenin.
keywords:
- how to create chart
- excel chart to image
- convert excel chart
- aspose cells chart
- how to export chart
- create chart java
title: Aspose.Cells Kullanarak Java’da Grafik Oluşturma ve Görüntü Olarak Dışa Aktarma
  – Tam Bir Kılavuz
url: /tr/java/charts-graphs/aspose-cells-java-create-export-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells Kullanarak Grafik Oluşturma ve Görüntü Olarak Dışa Aktarma – Tam Kılavuz

## Giriş

Java kodundan doğrudan **how to create chart** nesneleri oluşturmanın güvenilir bir yolunu arıyorsanız, Aspose.Cells for Java bunu basit hale getirir. Bu öğreticide bir piramit grafiği nasıl oluşturacağınızı, yüksek çözünürlüklü görüntü çıktısını nasıl yapılandıracağınızı ve sonunda grafiği PNG görüntüsü olarak nasıl dışa aktaracağınızı öğreneceksiniz. Sonunda **convert excel chart**'ı bir görüntü dosyasına nasıl dönüştüreceğinizi ve bu yaklaşımın otomatik raporlama için neden ideal olduğunu da anlayacaksınız.

**What You’ll Learn**  
- Aspose.Cells for Java'ı kurma  
- Java kullanarak bir Excel çalışma kitabında piramit grafiği oluşturma  
- Yüksek kaliteli renderleme için görüntü çıkış seçeneklerini yapılandırma  
- Grafikleri gösterge panoları, e‑postalar veya PDF'ler için görüntü olarak dışa aktarma  

Şimdi ön koşullara göz atalım ve ortamınızı hazırlayalım.

## Hızlı Yanıtlar
- **Gerekli kütüphane nedir?** Aspose.Cells for Java (v25.3+)  
- **Hangi grafik türü gösteriliyor?** Piramit grafik (başka bir türe geçebilirsiniz)  
- **Grafik nasıl dışa aktarılır?** `Chart.toImage()` ve `ImageOrPrintOptions` kullanın  
- **Diğer formatlara dışa aktarabilir miyim?** Evet – PNG, JPEG, BMP, GIF ve TIFF desteklenir  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme lisansı çalışır; üretim için ticari lisans gereklidir  

## Aspose.Cells ile “how to create chart” nedir?
Aspose.Cells, geliştiricilerin programlı olarak Excel çalışma sayfaları oluşturmasına, grafik eklemesine ve bunları görüntü olarak render etmesine olanak tanıyan zengin bir API sağlar—Microsoft Office yüklü olmasına gerek kalmadan. Bu, sunucu tarafı raporlama, veri analitiği gösterge panoları ve otomatik belge oluşturma için mükemmeldir.

## Excel grafiğini görüntüye dönüştürmek için Aspose.Cells neden kullanılmalı?
- **Office bağımlılığı yok:** Java destekleyen herhangi bir platformda çalışır.  
- **Yüksek doğrulukta renderleme:** Keskin görüntüler için anti-aliasing ve DPI ayarlarını destekler.  
- **Geniş format desteği:** PNG, JPEG, SVG, PDF ve daha fazlasına dışa aktarım.  
- **Performansa odaklı:** Büyük çalışma kitaplarıyla verimli çalışır ve çok iş parçacığıyla birleştirilebilir.  

## Ön Koşullar
- **Gerekli Kütüphaneler:** Aspose.Cells for Java sürüm 25.3 veya üstü.  
- **IDE:** IntelliJ IDEA, Eclipse veya herhangi bir Java uyumlu IDE.  
- **JDK:** Java 8 veya daha yenisi.  
- **Temel Bilgi:** Java, Maven/Gradle ve Excel dosya kavramlarına aşina olmak.  

## Aspose.Cells for Java Kurulumu

### Maven
Aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Bu satırı `build.gradle` dosyanıza ekleyin:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

**Lisans Edinme:** Aspose.Cells, ücretsiz bir deneme lisansı sunar; bunu [satın alma sayfasından](https://purchase.aspose.com/buy) edinebilirsiniz. Geliştirme sırasında tam işlevselliği açmak için geçici lisansı uygulayın.

### Temel Başlatma
Başlamak için bir `Workbook` örneği oluşturun. Bu nesne verilerinizi ve grafiğinizi tutacaktır:
```java
import com.aspose.cells.Workbook;

public class AsposeCellsInit {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        // Your chart creation code will go here.
    }
}
```

## Aspose.Cells ile Java'da Grafik Oluşturma

### Excel'de Piramit Grafik Oluşturma

#### Adım 1: Workbook ve Worksheet'i Başlatma
İlk olarak, çalışma kitabını ayarlayın ve varsayılan çalışma sayfasına bir referans alın.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY"; // Update with your directory path

Workbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

#### Adım 2: Piramit Grafik Ekleme
`ChartCollection` kullanarak bir piramit grafik ekleyin. Bu, **aspose cells chart** oluşturma sürecini gösterir.
```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

Worksheet sheet = worksheets.get(0);
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.PYRAMID, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);
```

## Görüntü Çıktı Seçeneklerini Yapılandırma (Grafik Nasıl Dışa Aktarılır)

### Adım 1: Çözünürlük ve Antialiasing Ayarlama
Keskin bir **excel chart to image** dönüşümü için render ayarlarını ince ayar yapın.
```java
import com.aspose.cells.ImageOrPrintOptions;
import java.awt.RenderingHints;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setVerticalResolution(300);
options.setHorizontalResolution(300);
options.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
options.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING, RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
```

## Grafiği Görüntü Olarak Dışa Aktarma (Excel Grafiğini Dönüştürme)

### Adım 1: Grafiği Görüntü Olarak Kaydet
Son olarak, daha önce yapılandırılmış seçenekleri kullanarak grafiği bir PNG dosyasına yazın.
```java
chart.toImage(dataDir + "chart.png", options);
```

**Sorun Giderme İpuçları**
- `dataDir`'in yazılabilir bir klasöre işaret ettiğini doğrulayın.  
- Aspose.Cells sürümünüzün 25.3 veya daha yeni olduğundan emin olun; eski sürümler burada kullanılan `toImage` aşırı yüklemesini içermeyebilir.  

## Pratik Uygulamalar
İşte **how to export chart** yeteneklerinin öne çıktığı yaygın senaryolar:
1. **İş Raporlaması:** Aylık satış gösterge panolarını otomatik olarak oluşturun.  
2. **Eğitim Araçları:** Öğrenciler için görsel performans raporları oluşturun.  
3. **Sağlık Analitiği:** Sunumlar için hasta istatistiklerini manuel Excel çalışması olmadan render edin.  

Bu kullanım durumları, geliştiricilerin sunucu tarafı grafik oluşturma ve görüntü dışa aktarma için neden Aspose.Cells'i tercih ettiğini gösterir.

## Performans Düşünceleri
Ölçek büyütürken:
- Kullanılmayan `Workbook` nesnelerini serbest bırakın.  
- Büyük veri setleri için akış API'lerini kullanın.  
- Birçok raporu aynı anda üretirken grafik oluşturmayı paralelleştirin.  

Bu ipuçlarını izlemek, Java hizmetinizin yoğun yük altında bile yanıt vermeye devam etmesini sağlar.

## Sonuç
Artık **how to create chart** nesneleri oluşturma, render ayarlarını özelleştirme ve Aspose.Cells for Java kullanarak **export chart** görüntülerini dışa aktarma konusunda sağlam bir temele sahipsiniz. Diğer `ChartType` değerleriyle deney yapın, stil uygulayın veya PNG çıktısını PDF'lere, web sayfalarına veya e‑posta eklerine entegre edin.

**Sonraki Adımlar**
- `ChartType.PYRAMID`'i değiştirerek çizgi, çubuk veya pasta grafikleri deneyin.  
- Başlık, lejand ve eksen özelleştirmesi için `Chart` sınıfını keşfedin.  
- Daha derin bilgiler için topluluğa katılın.  

Ek ipuçları ve gerçek dünya örnekleri için [Aspose forumunu](https://forum.aspose.com/c/cells/9) ziyaret etmeyi düşünün.

## Sıkça Sorulan Sorular

**S: Farklı bir grafik türü nasıl eklenir?**  
C: `ChartType` enum'undan başka bir değer kullanın, örneğin `ChartType.BAR` veya `ChartType.PIE`.

**S: Mevcut bir Excel dosyasından grafik oluşturabilir miyim?**  
C: Evet. `new Workbook("existing.xlsx")` ile çalışma kitabını yükleyin ve ardından grafik ekleyin veya değiştirin.

**S: **excel chart to image** kullanırken yaygın tuzaklar nelerdir?**  
C: Yanlış dosya yolları, yetersiz yazma izinleri veya Aspose.Cells'in 25.3'ten eski bir sürümünü kullanmak.

**S: Çok büyük çalışma kitaplarını verimli bir şekilde nasıl yönetebilirim?**  
C: Aspose.Cells'in akış API'lerini kullanın ve bellek kullanımını düşük tutmak için nesneleri zamanında serbest bırakın.

**S: Grafik başlıkları veya lejandları özelleştirmek mümkün mü?**  
C: Kesinlikle. `Chart` sınıfı `setTitle()`, `setLegend()` ve `setSeries()` gibi tam özelleştirme sağlayan metodlar sunar.

---

**Last Updated:** 2026-04-05  
**Tested With:** Aspose.Cells for Java 25.3  
**Author:** Aspose  

**Resources**
- [Dokümantasyon](https://reference.aspose.com/cells/java/)
- [Aspose.Cells for Java İndir](https://releases.aspose.com/cells/java/)
- [Lisans Satın Al](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme İndir](https://releases.aspose.com/cells/java/)
- [Geçici Lisans Al](https://purchase.aspose.com/temporary-license/)
- [Destek Forumu](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}