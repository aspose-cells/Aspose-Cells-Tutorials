---
date: '2026-04-08'
description: Aspose.Cells kullanarak Java'da sütun grafik oluşturmayı öğrenin; grafik
  oluşturma Java, grafik sayfası ekleme ve çalışma kitabını Excel olarak dışa aktarma
  konularını kapsar.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Aspose.Cells Java Öğreticisi ile Sütun Grafiği Oluşturma
url: /tr/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java ile Sütun Grafiği Oluşturma

Günümüzün veri odaklı uygulamalarında, **sütun grafiği oluşturmak** hızlı ve programlı bir şekilde ham sayıları net görsel içgörülere dönüştürebilir. Raporlama panosu, analiz aracı ya da basit bir dışa aktarma özelliği oluşturuyor olsanız da, Aspose.Cells for Java, Excel kullanıcı arayüzüyle uğraşmadan **chart java oluşturmak** projeleri için akıcı bir API sunar. Bu öğreticide, kütüphaneyi nasıl kuracağınızı, **Excel hücrelerini doldurmayı**, bir **grafik sayfası** eklemeyi, **grafik başlığını** özelleştirmeyi ve sonunda **workbook excel'i** bir dosyaya **dışa aktarmayı** öğreneceksiniz.

## Hızlı Yanıtlar
- **“generate column chart” ne anlama geliyor?** Tablo verilerinden dikey çubuk tipi bir görselleştirme oluşturur.  
- **Hangi kütüphane gereklidir?** Aspose.Cells for Java (ücretsiz deneme mevcut).  
- **Excel kurulumu gerekli mi?** Hayır, kütüphane Microsoft Excel'den bağımsız çalışır.  
- **XLS dışındaki formatlara dışa aktarabilir miyim?** Evet – PDF, PNG, SVG vb., `workbook.save()` ile.  
- **Üretim için lisans zorunlu mu?** Evet, satın alınmış veya geçici bir lisans gereklidir.

## Generate column chart nedir?
Sütun grafiği, veri serilerini dikey çubuklar olarak gösterir ve bölgeler, aylar veya ürün hatları gibi kategoriler arasında değerleri karşılaştırmayı kolaylaştırır. Aspose.Cells, bu grafiği tamamen kod içinde oluşturmanıza olanak tanır ve veri, stil ve çıktı formatı üzerinde tam kontrol sağlar.

## Neden Aspose.Cells kullanarak chart java oluşturmalısınız?
- **COM etkileşimi yok** – JVM'li herhangi bir işletim sisteminde çalışır.  
- **Zengin stil seçenekleri** – görüntüler, degrade geçişler, lejandlar ve özel yazı tipleri.  
- **Yüksek performans** – büyük veri setleri için uygundur.  
- **Birden çok dışa aktarma formatı** – XLS, XLSX, PDF, PNG ve daha fazlası.

## Önkoşullar
- **Java Development Kit (JDK) 8+** yüklü.  
- Temel Java bilgisi ve Excel kavramlarına aşinalık.  

### Gerekli Kütüphaneler
Aspose.Cells'i projenize aşağıdaki kod parçacıklarından birini kullanarak ekleyin.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Lisans Edinimi
Aspose, kapsamlı testler için ücretsiz deneme ve geçici bir lisans sunar.

- **Ücretsiz Deneme**: [Ücretsiz İndir](https://releases.aspose.com/cells/java/)  
- **Geçici Lisans**: [Buradan Talep Edin](https://purchase.aspose.com/temporary-license/)

## Aspose.Cells for Java Kurulumu

İlk olarak, bir `Workbook` örneği oluşturun – bu, veri ve grafiğimiz için bir tuval olacaktır.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Adım Adım Kılavuz

### 1. Çalışma Sayfası Oluşturma ve Adlandırma
Ham verileri **Data** adlı bir sayfada saklayacağız.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Excel Hücrelerini Doldurma
Sütun grafiğinin görselleştireceği bölge adlarını ve satış rakamlarını ekleyin.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Grafik Sayfası Ekleme
Grafiği ham veriden ayırmak, çalışma kitabını düzenli tutar.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Sütun Grafiği Oluşturma
Şimdi gerçekten **generate column chart** nesnelerini oluşturuyoruz.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Çizim Alanında Arka Plan Doldurması Olarak Resim Ayarlama
Arka plan resmi, grafiğin öne çıkmasını sağlayabilir.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Grafik Başlığını Ayarlama
**set chart title** özelleştirmek, okunabilirliği artırır.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Seri Verilerini ve Lejandı Yapılandırma
Veri aralığını grafiğe bağlayın ve lejandı konumlandırın.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Workbook Excel'i Dışa Aktarma
Son olarak, **export workbook excel** bir XLS dosyasına (veya desteklenen herhangi bir formata) dışa aktarın.

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Pratik Uygulamalar
- **İş Raporları** – Aylık PDF'ler için satış grafiklerini otomatik oluşturur.  
- **Veri Analiz Araçları** – Özel analiz panolarına dinamik grafikler yerleştirir.  
- **Kurumsal Panolar** – Gerçek zamanlı izleme için grafik görüntülerini anında yeniler.

## Performans Düşünceleri
- Büyük veri setleriyle çalışırken aşırı yükü azaltmak için hücre güncellemelerini toplu yapın.  
- Bir döngüde birçok çalışma kitabı işliyorsanız kaynakları (`workbook.dispose()`) serbest bırakın.  

## Yaygın Sorunlar ve Çözümler
- **Görsel görünmüyor** – Dosya yolunu ve görüntü formatının (PNG, JPEG) desteklendiğini doğrulayın.  
- **Grafik boş görünüyor** – Veri aralığı referanslarının (`Data!B2:B8`) doldurulmuş hücrelerle eşleştiğinden emin olun.  
- **Bellek yetersizliği hataları** – Verileri parçalar halinde işleyin ve büyük kayıtlardan sonra `System.gc()` çağırın.

## Sıkça Sorulan Sorular

**Q:** Bir sütun grafiğine birden fazla seri nasıl eklenir?  
**A:** `chart.getNSeries().add()` metodunu farklı veri aralıklarıyla tekrarlayarak çağırın, örneğin ikinci seri için `"Data!C2:C8"`.

**Q:** Eksen etiketlerini değiştirebilir miyim?  
**A:** Evet. `chart.getCategoryAxis().setTitle("Regions")` ve `chart.getValueAxis().setTitle("Sales")` metodlarını kullanın.

**Q:** XLS dışındaki hangi formatlara dışa aktarabilirim?  
**A:** PDF, PNG ve XLSX için sırasıyla `workbook.save("chart.pdf")`, `workbook.save("chart.png")` veya `workbook.save("chart.xlsx")` metodlarını kullanın.

**Q:** Geliştirme sürümleri için lisans gerekli mi?  
**A:** Ücretsiz deneme değerlendirme için çalışır, ancak üretim dağıtımları için kalıcı veya geçici bir lisans gereklidir.

**Q:** Binlerce satır için render hızını nasıl artırabilirim?  
**A:** Hücreleri `cells.importArray()` ile doldurun ve tüm veri yüklendikten sonra grafiği oluşturarak grafik yeniden çizimlerini en aza indirin.

---

**Son Güncelleme:** 2026-04-08  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

## Kaynaklar

- [Aspose.Cells Dokümantasyonu](https://reference.aspose.com/cells/java/)
- [Aspose.Cells İndir](https://releases.aspose.com/cells/java/)
- [Lisans Satın Al](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme](https://releases.aspose.com/cells/java/)
- [Geçici Lisans Talebi](https://purchase.aspose.com/temporary-license/)
- [Destek Forumu](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}