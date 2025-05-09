---
"date": "2025-04-08"
"description": "Java için Aspose.Cells kullanarak pasta grafikleri oluşturmayı ve özelleştirmeyi öğrenin. Geliştiriciler için kod örnekleri içeren adım adım bir kılavuz."
"title": "Aspose.Cells&#58;te Ustalaşma Java'da Pasta Grafikleri Oluşturma ve Özelleştirme"
"url": "/tr/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells'e Hakim Olmak: Java'da Pasta Grafikleri Oluşturma ve Özelleştirme

## giriiş
Excel'de veri görselleştirmeyle uğraşırken görsel olarak çekici grafikler oluşturmak yaygın bir gerekliliktir. İster demografik bilgiler sunuyor olun ister piyasa eğilimlerini analiz ediyor olun, pasta grafikleri orantılı verileri temsil etmenin net bir yolunu sunar. Ancak, bu grafikleri programatik olarak ayarlamak karmaşık olabilir. Bu eğitim, Java kullanarak bir Aspose.Cells Pasta Grafiği oluşturma ve özelleştirme konusunda size rehberlik ederek geliştiriciler için süreci basitleştirir.

**Ne Öğreneceksiniz:**
- Ortamınızı Java için Aspose.Cells ile ayarlayın.
- Yeni bir çalışma kitabı oluşturun ve çalışma sayfası hücrelerine erişin.
- Grafik oluşturmaya hazırlanmak için verileri belirli hücrelere doldurun.
- Bu verilerden bir pasta grafiği oluşturun.
- Renkler, başlıklar ve açıklamalar dahil olmak üzere pasta grafiğinizin görünümünü özelleştirin.

Dalmadan önce, Java programlama ve Maven veya Gradle bağımlılık yönetimi hakkında temel bir anlayışa sahip olduğunuzdan emin olun. Ortamımızı ayarlayalım!

## Ön koşullar
Bu eğitimi takip etmek için şunlara ihtiyacınız olacak:
- **Java Geliştirme Kiti (JDK)**: Sürüm 8 veya üzeri.
- **Entegre Geliştirme Ortamı (IDE)**: IntelliJ IDEA veya Eclipse gibi.
- **Bağımlılık Yönetimi**: Bağımlılıklarınızı yönetmek için Maven veya Gradle kullanın.

### Gerekli Kütüphaneler ve Bağımlılıklar
Maven veya Gradle kullanarak projenize Aspose.Cells for Java'yı eklemeyi unutmayın.

**Usta**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Lisans Edinme Adımları
Aspose.Cells for Java ticari bir kütüphanedir, ancak ücretsiz denemeyle başlayabilir veya geçici bir lisans için başvurabilirsiniz. Ziyaret edin [satın alma sayfası](https://purchase.aspose.com/buy) lisanslama seçeneklerini keşfetmek için.

## Java için Aspose.Cells Kurulumu
Öncelikle, proje ortamınızın gerekli kütüphaneleri içerdiğinden emin olun, bunları yukarıda gösterildiği gibi Maven veya Gradle aracılığıyla ekleyin. Dahil ettikten sonra, Aspose.Cells'i başlatabilirsiniz:

```java
import com.aspose.cells.Workbook;

// Yeni bir çalışma kitabı örneği başlatın
Workbook workbook = new Workbook();
```

## Uygulama Kılavuzu

### Bir Çalışma Kitabı Oluşturun ve Yapılandırın
Çalışma kitabı oluşturmak, verilerinizi ayarlayacağınız ilk adımdır.

#### Kütüphaneleri içe aktar
Bu içe aktarımların dosyanızın en üstüne eklendiğinden emin olun:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Adım 1: Bir Çalışma Kitabı Örneği Oluşturun
```java
// Üzerinde çalışılacak boş bir çalışma kitabı örneği oluşturur.
Workbook workbook = new Workbook();
```
Bu adım Excel dosyanızı programlı olarak başlatır ve Aspose.Cells işlevlerini kullanarak dosyanızda değişiklik yapmanıza olanak tanır.

### Çalışma Sayfası Hücrelerine Erişim veya Değişiklik Yapma
Daha sonra pasta grafiğinde kullanılacak çalışma sayfası hücrelerine veri girin.

#### Adım 2: Bir Çalışma Sayfasına ve Hücrelerine Erişim
```java
// Çalışma kitabındaki ilk çalışma sayfasına erişin.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Pasta grafiğinde kullanılan örnek değerleri belirli hücrelere yerleştirin.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Pasta grafiğinin yüzde değerlerini belirli hücrelere yerleştirin.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Burada, çalışma sayfasını pasta grafiğinin farklı bölümlerini temsil edecek verilerle dolduracaksınız.

### Pasta Grafiği Oluşturun

#### Adım 3: Çalışma Sayfasına Pasta Grafiği Ekleyin
```java
// Çalışma sayfasında bir pasta grafiği oluşturun.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Bu adım, çalışma sayfanıza belirtilen konumlarda ve boyutlarda yeni bir pasta grafiği ekler.

### Pasta Grafik Serilerini ve Verilerini Yapılandırın

#### Adım 4: Grafik için Seriyi Ayarlayın
```java
// Grafik için seri veri aralığını yapılandırın.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Pasta grafiği başlığını, başlık metnini içeren hücreye bağlayın.
pie.getTitle().setLinkedSource("D2");
```
Bu kod veri aralığınızı birbirine bağlar ve pasta grafiği için seriyi ayarlar.

### Grafik Efsanesini ve Başlık Görünümünü Yapılandırın

#### Adım 5: Grafik Efsanesini ve Başlığını Özelleştirin
```java
// Efsane konumunu grafiğin en altına ayarlayın.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Grafik başlığı için yazı tipi özelliklerini ayarlayın.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Görünümün özelleştirilmesi okunabilirliği ve görsel çekiciliği artırır.

### Grafik Serisi Renklerini Özelleştir

#### Adım 6: Pasta Segmenti Renklerini Değiştirin
```java
import com.aspose.cells.Color;

// Bireysel pasta grafiği segmentlerinin renklerine erişin ve bunları özelleştirin.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Bu ayarlar, grafiğinizi belirli renk düzenlerine uyacak şekilde kişiselleştirir.

### Sütunları Otomatik Olarak Sığdır ve Çalışma Kitabını Kaydet

#### Adım 7: Sütun Genişliklerini Ayarlayın ve Dosyayı Kaydedin
```java
// Tüm sütunları otomatik olarak sığdır.
worksheet.autoFitColumns();

// Çalışma kitabını kaydetmek için çıktı dizini yer tutucu yolunu tanımlayın.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Değiştirilen çalışma kitabını belirtilen dizindeki bir Excel dosyasına kaydedin.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Son olarak sütunları otomatik olarak sığdırın ve çalışma kitabınızı kaydedin.

## Pratik Uygulamalar
1. **Demografik Analiz**: Nüfus dağılımlarını farklı ülkeler veya bölgelerde göstermek için pasta grafiklerini kullanın.
2. **Pazar Payı Raporları**:Bir sektördeki farklı şirketlerin pazar paylarını gösterin.
3. **Bütçe Tahsisi**:Bir organizasyon içindeki çeşitli departmanlara bütçelerin nasıl dağıtıldığını görselleştirin.

Bu uygulamalar Aspose.Cells'in gerçek dünya senaryolarındaki çok yönlülüğünü ve faydasını göstermektedir.

## Performans Hususları
Aspose.Cells kullanırken performansı optimize etmek için:
- Artık ihtiyaç duyulmayan nesnelerden kurtularak bellek kullanımını en aza indirin.
- Büyük veri kümelerini işlemek için verimli veri yapıları kullanın.
- Darboğazları belirlemek için uygulamanızın profilini çıkarın.

En iyi uygulamalara bağlı kalmak, sorunsuz ve duyarlı uygulamaların garantisidir.

## Çözüm
Bu eğitim, Java'da Aspose.Cells kullanarak bir pasta grafiği oluşturma ve özelleştirme adımlarında size yol gösterdi. Bu bilgiyle, artık bu teknikleri projelerinizdeki çeşitli veri görselleştirme görevlerine uygulayabilirsiniz. Daha fazla araştırma için, Aspose.Cells ile kullanılabilen ek grafik türlerine ve gelişmiş özelleştirme seçeneklerine dalmayı düşünün.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}