---
"date": "2025-04-07"
"description": "Aspose.Cells for Java kullanarak Excel'de grafiklerin nasıl oluşturulacağını ve özelleştirileceğini öğrenin. Bu ayrıntılı kılavuzla grafik oluşturmayı otomatikleştirin, veri görselleştirmeyi geliştirin ve zamandan tasarruf edin."
"title": "Aspose.Cells Java ile Excel Grafikleri Oluşturma ve Şekillendirme Kapsamlı Bir Kılavuz"
"url": "/tr/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells Java ile Excel Grafikleri Oluşturma ve Şekillendirme

## giriiş

Günümüzün veri odaklı dünyasında, etkili bilgi görselleştirmesi analiz ve karar alma için hayati önem taşır. Genellikle, Excel çalışma kitaplarında dinamik grafiklerin programatik olarak oluşturulması gerekir; özellikle büyük veri kümeleri veya otomatik raporlama sistemleriyle uğraşırken. Bu eğitim, Excel'de grafikleri sorunsuz bir şekilde oluşturmak ve özelleştirmek için Java için Aspose.Cells'in nasıl kullanılacağını gösterir. Aspose.Cells'i Java uygulamalarınıza entegre ederek, grafik oluşturmayı otomatikleştirebilir, veri sunumunu iyileştirebilir ve zamandan tasarruf edebilirsiniz.

**Ne Öğreneceksiniz:**
- Aspose.Cells kullanarak bir çalışma kitabını başlatma ve onu verilerle doldurma.
- Veri işaretleyicileri ile çizgi grafikleri oluşturma ve yapılandırma.
- Daha iyi görselleştirme için seri görünümünü ve renklerini özelleştirme.
- Yeni oluşturulan grafikle birlikte çalışma kitabını Excel formatında kaydedin.

Başlamak için gereken ön koşulları tartışarak başlayalım.

## Ön koşullar

Java için Aspose.Cells'i kullanarak grafikler oluşturup biçimlendirmeden önce, aşağıdaki ayarların yapıldığından emin olun:

### Gerekli Kütüphaneler
Projenize Aspose.Cells'i bir bağımlılık olarak ekleyin. İşte hem Maven hem de Gradle kullanıcıları için talimatlar:

**Usta:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Çevre Kurulum Gereksinimleri
- Sisteminizde Java Development Kit (JDK) yüklü.
- Kodlama ve test için IntelliJ IDEA veya Eclipse gibi Entegre Geliştirme Ortamı (IDE).

### Bilgi Önkoşulları
Temel Java programlama bilgisinin yanı sıra Excel çalışma kitapları ve grafik kavramlarına aşinalık da gereklidir. 

### Lisans Edinimi
Aspose.Cells, tam işlevsellik için lisans gerektiren ticari bir üründür. Özelliklerini değerlendirmek için ücretsiz bir deneme alabilir, genişletilmiş test için geçici bir lisans talep edebilir veya ürünü uzun süreli kullanım için satın alabilirsiniz.

- **Ücretsiz Deneme:** [Ücretsiz Denemeyi İndirin](https://releases.aspose.com/cells/java/)
- **Geçici Lisans:** [Geçici Lisans Talebi](https://purchase.aspose.com/temporary-license/)
- **Satın almak:** [Aspose.Cells'i satın alın](https://purchase.aspose.com/buy)

## Java için Aspose.Cells Kurulumu

Gerekli bağımlılıkları yükledikten sonra, geliştirme ortamınızı Aspose.Cells kullanacak şekilde ayarlayın. Kütüphaneyi içe aktararak ve Java uygulamanızda bir Workbook nesnesi başlatarak başlayın:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Yeni bir çalışma kitabı örneği başlatın
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Uygulama Kılavuzu

Bu bölümde, uygulamayı farklı özelliklere ayıracağız: Çalışma Kitabı Başlatma ve Veri Doldurma, Grafik Oluşturma ve Yapılandırma, Seri Özelleştirme ve Çalışma Kitabını Kaydetme.

### Özellik 1: Çalışma Kitabı Başlatma ve Veri Doldurma

**Genel Bakış:** Bu özellik, yeni bir çalışma kitabı oluşturmaya, ilk çalışma sayfasına erişmeye ve grafik oluşturma için verileri doldurmaya odaklanır.

#### Adım 1: Çalışma Kitabını Başlatın
Bir örnek oluşturarak başlayın `Workbook` nesne:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Bir çalışma kitabını örneklendirin
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Adım 2: Sütun Başlıklarını Ayarlayın ve Verileri Doldurun
Sütun başlıklarını tanımlayın ve satırları örnek verilerle doldurun:

```java
        // Sütun başlıklarını ayarla 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Seri 1 için rastgele veri oluşturun
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Seri 2 için rastgele veri oluşturun
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Özellik 2: Grafik Oluşturma ve Yapılandırma

**Genel Bakış:** Bu özellik, çalışma kitabının çalışma sayfasına bir grafik eklemeyi, stilini ayarlamayı ve temel özellikleri yapılandırmayı gösterir.

#### Adım 3: Çalışma Sayfasına Bir Grafik Ekleyin
Veri işaretleyicileri içeren bir çizgi grafiği ekleyin:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Bir çalışma kitabını örneklendirin
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Çalışma sayfasına grafik ekle
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Grafiğe erişin ve yapılandırın
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Önceden tanımlanmış bir stil ayarlayın
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Özellik 3: Seri Yapılandırma ve Özelleştirme

**Genel Bakış:** Çeşitli renkler ve işaretçi stilleri gibi seri ayarlarını özelleştirerek grafiklerinizin görsel çekiciliğini artırın.

#### Adım 4: Seri Ayarlarını Özelleştirin
Seri verilerini yapılandırın, özel biçimlendirme uygulayın ve işaretleyicileri ayarlayın:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Bir çalışma kitabını örneklendirin
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Seriyi grafiğe ekle
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Seri noktaları için çeşitli renkleri etkinleştirin
        chart.getNSeries().setColorVaried(true);

        // İlk seri işaretleyici stillerini ve renklerini özelleştirin
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // İlk seri için X ve Y değerlerini ayarlayın
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // İkinci seri işaretleyici stillerini ve renklerini özelleştirin
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // İkinci seri için X ve Y değerlerini ayarlayın
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Özellik 4: Çalışma Kitabı Kaydetme

**Genel Bakış:** Son olarak, değişikliklerinizi kalıcı hale getirmek için çalışma kitabını kaydedin ve grafiğin Excel dosyasına dahil edildiğinden emin olun.

#### Adım 5: Çalışma Kitabını Kaydedin
Yeni oluşturulan grafiklerle çalışma kitabınızı kaydedin:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Bir çalışma kitabını örneklendirin
        Workbook workbook = new Workbook();
        
        // İlk çalışma sayfasına erişin ve önceki adımlarda olduğu gibi veri ve grafik yapılandırmasını ekleyin...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Veri ekleme ve grafik yapılandırmasının uygulanması burada olacaktır)

        // Çalışma kitabını bir Excel dosyasına kaydedin
        workbook.save("StyledChart.xlsx");
    }
}
```

**Anahtar Kelime Önerileri:**
- "Java için Aspose.Cells"
- "Java ile Excel grafik oluşturma"
- "Excel otomasyonu için Java programlama"

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}