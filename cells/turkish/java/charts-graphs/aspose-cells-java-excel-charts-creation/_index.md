---
date: '2026-04-08'
description: Aspose.Cells for Java kullanarak işaretçili bir çizgi grafik oluşturmayı,
  grafiği çalışma sayfasına eklemeyi ve otomatik raporlama için Excel grafiklerini
  özelleştirmeyi öğrenin.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Aspose.Cells for Java Kullanarak İşaretçili Çizgi Grafiği Oluşturun
url: /tr/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java ile Excel Grafiklerini Oluşturma ve Stil Verme

## Giriş

Günümüzün veri odaklı dünyasında, **işaretçili bir çizgi grafiği**, eğilimleri ve aykırı değerleri görselleştirmenin en etkili yollarından biridir. Otomatik raporlar ya da günlük güncellenen bir gösterge paneli oluşturuyor olun, bir çalışma sayfasına programlı olarak işaretçili bir çizgi grafiği ekleyebilmek sayısız manuel adımı tasarruf ettirir. Bu öğreticide, Aspose.Cells for Java kullanarak bu tür grafikler oluşturmayı, stil vermeyi ve dışa aktarmayı adım adım gösteriyoruz, böylece zahmetli Excel işlemleri yerine içgörülere odaklanabilirsiniz.

**Öğrenecekleriniz**
- Aspose.Cells kullanarak bir çalışma kitabı başlatma ve veri ile doldurma.  
- **İşaretçili bir çizgi grafiğini bir çalışma sayfasına ekleme** ve görünümünü yapılandırma.  
- Seri renklerini, işaretçileri ve diğer stil seçeneklerini özelleştirme.  
- Stil verilen grafiği içeren bir Excel dosyası olarak çalışma kitabını kaydetme.

## Hızlı Yanıtlar
- **Başlamak için birincil sınıf nedir?** `Workbook` yeni bir Excel dosyası başlatır.  
- **Hangi grafik türü işaretçili bir çizgi grafiği oluşturur?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Seri noktaları için özel renkler nasıl ayarlanır?** `chart.getNSeries().setColorVaried(true)` kullanın ve işaretçi alan renklerini ayarlayın.  
- **Tam işlevsellik için lisansa ihtiyacım var mı?** Evet, ücretli veya geçici bir Aspose.Cells lisansı değerlendirme sınırlamalarını kaldırır.  
- **Sonucu XLSX olarak dışa aktarabilir miyim?** Kesinlikle—`workbook.save("StyledChart.xlsx")` bir XLSX dosyası oluşturur.

## Ön Koşullar

Aspose.Cells for Java kullanarak grafik oluşturup stil vermeden önce, aşağıdaki kurulumun yapıldığından emin olun:

### Gerekli Kütüphaneler
Projenize bir bağımlılık olarak Aspose.Cells ekleyin. İşte Maven ve Gradle kullanıcıları için talimatlar:

**Maven:**
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

### Ortam Kurulum Gereksinimleri
- Sisteminizde Java Development Kit (JDK) kurulu.  
- Kodlama ve test için IntelliJ IDEA veya Eclipse gibi bir Entegre Geliştirme Ortamı (IDE).

### Bilgi Ön Koşulları
Java programlamaya temel bir anlayış ve Excel çalışma kitapları ve grafik kavramlarına aşinalık gereklidir.

### Lisans Edinme
Aspose.Cells ticari bir üründür ve tam işlevsellik için lisans gerektirir. Özelliklerini değerlendirmek için ücretsiz bir deneme alabilir, uzun vadeli test için geçici bir lisans talep edebilir veya ürünü uzun vadeli kullanım için satın alabilirsiniz.

- **Ücretsiz Deneme İndir:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Geçici Lisans İste:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Aspose.Cells Satın Al:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Aspose.Cells for Java Kurulumu

Gerekli bağımlılıkları kurduktan sonra, geliştirme ortamınızı Aspose.Cells kullanacak şekilde ayarlayın. Kütüphaneyi içe aktararak ve Java uygulamanızda bir `Workbook` nesnesi başlatarak başlayın:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Uygulama Rehberi

Bu bölümde, uygulamayı ayrı özelliklere ayıracağız: Çalışma Kitabı Başlatma ve Veri Doldurma, Grafik Oluşturma ve Yapılandırma, Seri Özelleştirme ve Çalışma Kitabını Kaydetme.

### Özellik 1: Çalışma Kitabı Başlatma ve Veri Doldurma

**Genel Bakış:** Bu özellik, yeni bir çalışma kitabı oluşturmayı, ilk çalışma sayfasına erişmeyi ve grafik oluşturmak için veri doldurmayı hedefler.

#### Adım 1: Çalışma Kitabını Başlat
Bir `Workbook` nesnesi örnekleyerek başlayın:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Adım 2: Sütun Başlıklarını Ayarla ve Verileri Doldur
Sütun başlıklarını tanımlayın ve örnek verilerle satırları doldurun:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Özellik 2: Grafik Oluşturma ve Yapılandırma

**Genel Bakış:** Bu özellik, çalışma kitabının çalışma sayfasına bir grafik eklemeyi, stilini ayarlamayı ve temel özellikleri yapılandırmayı gösterir.

#### Adım 3: Çalışma Sayfasına Bir Grafik Ekle
İşaretçili bir çizgi grafiği ekleyin:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Özellik 3: Seri Yapılandırması ve Özelleştirme

**Genel Bakış:** Serilerin renklerini çeşitlendirme ve işaretçi stillerini özelleştirerek grafiklerinizin görsel çekiciliğini artırın.

#### Adım 4: Seri Ayarlarını Özelleştir
Seri verilerini yapılandırın, özel biçimlendirme uygulayın ve işaretçileri ayarlayın:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Özellik 4: Çalışma Kitabını Kaydetme

**Genel Bakış:** Son olarak, değişikliklerinizi kalıcı hale getirmek ve grafiğin Excel dosyasına dahil edildiğinden emin olmak için çalışma kitabını kaydedin.

#### Adım 5: Çalışma Kitabını Kaydet
Yeni oluşturulan grafiklerle çalışma kitabınızı kaydedin:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Yaygın Sorunlar ve Sorun Giderme

- **Grafik boş görünüyor:** `setXValues` ve `setValues` içinde kullanılan hücre aralıklarının doldurulmuş hücrelere doğru referans verdiğinden emin olun.  
- **Renkler uygulanmadı:** `chart.getNSeries().setColorVaried(true)` çağrısının bireysel serileri özelleştirmeden önce yapıldığını doğrulayın.  
- **Lisans hataları:** Deneme lisansı grafik sayısını sınırlayabilir; kısıtlamaları kaldırmak için tam lisans yükleyin.

## Sıkça Sorulan Sorular

**S: Aspose.Cells ile başka grafik türleri (ör. çubuk, pasta) oluşturabilir miyim?**  
C: Evet, Aspose.Cells geniş bir grafik yelpazesi destekler; sadece `ChartType.LINE_WITH_DATA_MARKERS` ifadesini istediğiniz enum değeriyle değiştirin.

**S: Çalışma kitabını kapatmam veya kaynakları serbest bırakmam gerekiyor mu?**  
C: `Workbook` sınıfı kaynakları otomatik yönetir, ancak uzun süren uygulamalarda belleği boşaltmak için `workbook.dispose()` çağırabilirsiniz.

**S: Aynı çalışma sayfasına birden fazla grafik eklemek mümkün mü?**  
C: Kesinlikle—eklemek istediğiniz her grafik için `worksheet.getCharts().add(...)` çağırın.

**S: Dosyayı eski bir Excel formatı (XLS) olarak nasıl dışa aktarırım?**  
C: `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);` ifadesini kullanın.

**S: Grafik, Microsoft Excel'de açıldığında stilini korur mu?**  
C: Evet, Aspose.Cells yerel Excel grafik nesneleri yazar, bu yüzden tüm stiller, renkler ve işaretçiler tanımlandığı gibi görünür.

---

**Son Güncelleme:** 2026-04-08  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}