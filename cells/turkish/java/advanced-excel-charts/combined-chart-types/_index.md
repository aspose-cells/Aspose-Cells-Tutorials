---
date: 2026-09-02
description: Aspose.Cells for Java kullanarak grafiği PNG olarak dışa aktarmayı, data
  series eklemeyi, line column chart birleştirmeyi, çalışma kitabını XLSX olarak kaydetmeyi
  ve legend chart eklemeyi öğrenin.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Grafiği PNG olarak dışa aktar ve birleşik grafik için data series ekle
og_description: Aspose.Cells for Java ile grafiği PNG olarak dışa aktar, line and
  column chart birleştir, data series ekle ve çalışma kitabını XLSX olarak tek bir
  öğreticide kaydet.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Grafiği PNG olarak dışa aktar ve birleşik grafik için data series ekle
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Grafiği PNG olarak dışa aktar ve birleşik grafik için data series ekle
url: /tr/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiği PNG olarak dışa aktar ve birleşik grafik için veri serisi ekle

Bu öğreticide Excel çalışma kitabına **veri serisi ekle**, **çizgi ve sütun grafiğini birleştir** ve Aspose.Cells for Java kullanarak **grafiği PNG olarak dışa aktar** öğreneceksiniz. Çalışma kitabını kurmaktan, bir çalışma sayfasına grafiği eklemeye, lejandı özelleştirmeye, **çalışma kitabını XLSX olarak kaydet** ve grafiğin PNG görüntüsünü oluşturmaya kadar her adımı adım adım göstereceğiz. Sonunda, raporlara veya panolara yerleştirebileceğiniz hazır bir birleşik grafik elde edeceksiniz.

## Hızlı cevaplar
- **Birleşik grafikleri hangi kütüphane oluşturur?** Aspose.Cells for Java.  
- **Veri serisi nasıl eklenir?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **Grafik PNG olarak nasıl dışa aktarılır?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Çalışma kitabını hangi dosya formatında kaydedebilirim?** Standard `.xlsx` (save workbook as XLSX).  
- **Üretim için lisans gerekli mi?** Yes – a valid Aspose.Cells license is required for production deployments.

## Aspose.Cells'ta grafik PNG olarak dışa aktarılması nedir?
Grafiği PNG olarak dışa aktarmak, Excel grafiğinin bir raster görüntüsünü oluşturur; bu görüntü web sayfalarında, raporlarda veya e-postalarda Excel uygulamasına ihtiyaç duymadan gösterilebilir. Bu yöntem, tam görsel düzeni, renkleri ve veri işaretçilerini yakalayarak taşınabilir bir görüntü dosyası üretir.

## Neden birleşik çizgi-sütun grafiği oluşturmalıyız?
Birleşik çizgi‑sütun grafiği, farklı veri setlerini ayrı görsel temsillerle (ör. bir çizgi serisi bir sütun serisinin üzerine) tek bir görünümde göstermenizi sağlar. Bu yaklaşım, trendleri toplamlarla karşılaştırmak, korelasyonları vurgulamak veya daha zengin içgörüler sunarken görsel alanı küçük tutmak için idealdir.

## Önkoşullar
- Java Development Kit (JDK) 8 veya üzeri  
- Aspose.Cells for Java kütüphanesi (aşağıdaki bağlantıdan indirin)  
- Java sözdizimi ve Excel kavramlarına temel aşinalık  

## Başlarken

İlk olarak, resmi siteden Aspose.Cells for Java kütüphanesini indirin:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR dosyası projenizin sınıf yoluna eklendikten sonra, grafiği oluşturmaya başlayabilirsiniz.

### Adım 1: aspose.cells sınıflarını içe aktar
`Workbook`, Aspose.Cells'in bellekte bir Excel dosyasının tamamını temsil eden temel nesnesidir.  
```java
import com.aspose.cells.*;
```

### Adım 2: yeni bir çalışma kitabı oluştur
`Worksheet`, bir `Workbook` içinde tek bir sayfayı temsil eder ve hücrelere, satırlara ve grafiklere erişim sağlar.  
```java
Workbook workbook = new Workbook();
```

### Adım 3: ilk çalışma sayfasına eriş
`Chart`, tüm grafikle ilgili ayarları, serileri ve render seçeneklerini tutan nesnedir.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Adım 4: çalışma sayfasına birleşik bir grafik nesnesi ekle  
İlk olarak bir çizgi grafiği oluşturacağız ve daha sonra bir sütun serisi ekleyerek **birleşik çizgi‑sütun grafiği** etkisini elde edeceğiz.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Grafiğe veri ekleme

Grafik konteyneri oluşturulduğuna göre, ona veri beslememiz gerekiyor.

### Adım 5: veri aralıklarını tanımla ve veri serisi ekle
`NSeries`, bir grafik için her veri serisini saklayan koleksiyondur. Bir seri eklemek, hücre aralığını grafikle bağlar.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **İpucu:** İlk parametre (`"A1:A5"`), ilk seri için aralıktır ve ikinci parametre (`"B1:B5"`), ilk seriyle birleştirilecek ikinci seriyi oluşturur.

### Adım 6: kategori (X‑ekseni) verisini ayarla
`CategoryAxis`, grafiğin yatay eksenini temsil eder ve X‑ekseni boyunca gösterilen etiketleri kontrol eder.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Grafik özelleştirme

İyi bir grafik bir hikâye anlatır. Ona başlıklar, eksen etiketleri ve net bir lejant verelim.

### Adım 7: grafik eksen etiketlerini ve başlığını ayarla
`Title`, grafiğin ana başlığını ayarlar ve `Axis` nesneleri X ve Y eksenlerini temsil eder.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Adım 8: grafik lejantını ekle ve konumunu ayarla
`Legend`, grafikteki seri lejantının konumunu ve görünümünü kontrol eder.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Grafiği kaydetme ve dışa aktarma

Özelleştirmeden sonra, **çalışma kitabını XLSX olarak kaydet** ve ayrıca bir görüntü oluşturmak isteyeceksiniz.

### Adım 9: çalışma kitabını bir Excel dosyası (XLSX) olarak kaydet
`Workbook.save`, bellekteki çalışma kitabını belirtilen formatta bir dosyaya yazar.  
```java
workbook.save("CombinedChart.xlsx");
```

### Adım 10: grafiği PNG olarak dışa aktar
`Chart.toImage`, grafiği seçilen formatta bir görüntü dosyası olarak render eder.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` yöntemi **Excel grafiği** görüntülerini oluşturur; bu görüntüler web sayfalarında, raporlarda veya e-postalarda kullanılabilir.

## Yaygın sorunlar ve sorun giderme

| Sorun | Çözüm |
|-------|----------|
| **Veri görünmüyor** | Grafiği oluşturmadan önce hücre aralıklarının (`A1:A5`, `B1:B5`, `C1:C5`) gerçekten veri içerdiğini doğrulayın. |
| **Lejant grafikle çakışıyor** | `chart.getLegend().setOverlay(false)` ayarlayın veya lejantı farklı bir konuma taşıyın (ör. `RIGHT`). |
| **Görüntü dosyası boş** | Grafiğin en az bir serisi olduğundan ve `chart.toImage`'in tüm özelleştirmelerden sonra çağrıldığından emin olun. |
| **Kaydetme bir istisna fırlatıyor** | Hedef dizine yazma izninizin olduğundan ve dosyanın Excel'de açık olmadığından emin olun. |

## Sıkça sorulan sorular

**Q: Aspose.Cells for Java nasıl kurulur?**  
**A:** JAR'ı resmi siteden indirin ve projenizin sınıf yoluna ekleyin. İndirme bağlantısı: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Çizgi ve sütun dışındaki diğer grafik türlerini oluşturabilir miyim?**  
**A:** Evet, Aspose.Cells çubuk, pasta, dağılım, alan ve daha birçok grafik türünü destekler. Tam liste için API belgelerine bakın.

**Q: Üretim kullanımı için lisans gerekli mi?**  
**A:** Üretim dağıtımları için geçerli bir Aspose.Cells lisansı gereklidir. Değerlendirme için ücretsiz deneme sürümü mevcuttur.

**Q: Her bir serinin renklerini nasıl değiştirebilirim?**  
**A:** Seriyi ekledikten sonra `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (veya benzeri) kullanın.

**Q: Daha fazla kod örneği nerede bulunabilir?**  
**A:** Kapsamlı belgeler ve ek örnekler Aspose referans sitesinde mevcuttur: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Son güncelleme:** 2026-09-02  
**Test edilen sürüm:** Aspose.Cells for Java latest version  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.Cells for Java kullanarak Excel Grafiklerine Etiket Ekleme](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Aspose.Cells for Java kullanarak Trend Çizgili Excel Grafiği Oluşturma ve Görüntü Olarak Dışa Aktarma](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells for Java kullanarak Excel Grafiklerini PDF'ye Dışa Aktarma: Özel Sayfa Boyutları Rehberi](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}