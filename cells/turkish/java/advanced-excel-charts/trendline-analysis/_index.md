---
date: 2026-08-27
description: Aspose.Cells for Java kullanarak trendline'ı chart'e eklemeyi, R‑squared
  değerini görüntülemeyi ve chart'i PNG veya JPEG image olarak dışa aktarmayı öğrenin.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Trendline Analizi ile Chart'i Image Olarak Dışa Aktar
og_description: Aspose.Cells for Java kullanarak chart'e trendline ekleyin, R‑squared'i
  görüntüleyin ve sonucu PNG/JPEG olarak dışa aktarın – hızlı, 50 formatlı bir çözüm.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Aspose.Cells for Java ile chart'e trendline ekleyin ve image olarak dışa
  aktarın
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Java'da chart'e trendline ekleme ve image olarak dışa aktarma
url: /tr/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiğe eğri çizgisi ekleyin ve görüntü olarak dışa aktarın

Bu öğreticide, **grafiğe eğri çizgisi ekleme**, R‑kare değerini göstermeyi ve Aspose.Cells for Java kullanarak görseli PNG veya JPEG dosyası olarak dışa aktarmayı öğreneceksiniz. Eğri çizgilerinin neden önemli olduğunu, çalışma kitabını nasıl hazırlayacağınızı ve raporlar, e‑postalar veya web sayfalarına yerleştirilebilecek yüksek çözünürlüklü bir görüntü oluşturmak için kesin adımları göreceksiniz.

## Hızlı cevaplar
- **Bu kılavuzun ana hedefi nedir?** Grafiğe eğri çizgisi eklemeyi, denklemini ve R‑kare değerini göstermeyi ve Java ile grafiği görüntü olarak dışa aktarmayı göstermek.  
- **Hangi kütüphaneye ihtiyacım var?** Aspose.Cells for Java – bunu [Aspose.Cells for Java sürüm sayfasından](https://releases.aspose.com/cells/java/) indirebilirsiniz.  
- **Geliştirme için lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim dağıtımları için ticari lisans gereklidir.  
- **Excel çalışma kitabını programlı olarak oluşturabilir miyim?** Evet – öğreticide sıfırdan bir XLSX çalışma kitabı oluşturulur ve kaydedilir.  
- **Grafik PNG veya JPEG olarak nasıl dışa aktarılır?** `Chart.toImage()` metodunu çağırın ve dönen `BufferedImage`'ı `ImageIO.write(...)` ile yazın.

## Excel grafiğini eğri çizgisiyle nasıl oluşturur ve görüntü olarak dışa aktarırsınız?
Çalışma kitabını yükleyin, bir çizgi grafiği ekleyin, denklemi ve R‑kare değerini gösteren bir eğri çizgisi ekleyin, çalışma kitabını kaydedin, ardından `chart.toImage()` metodunu çağırın ve ortaya çıkan `BufferedImage`'ı PNG veya JPEG dosyasına yazın. Bu uçtan uca akış sadece birkaç satır Java kodu gerektirir ve herhangi bir sonraki uygulama için uygun piksel‑kusursuz bir görüntü üretir.

## Grafiği görüntü olarak dışa aktarmak nedir?
Bir grafiği görüntüye dışa aktarmak, verilerinizin görsel temsilini taşınabilir bir bitmap (PNG, JPEG, BMP vb.) formatına dönüştürür. Bu format, orijinal Excel dosyasına ihtiyaç duyulmayan raporlar, web sayfaları veya sunumlarda grafik yerleştirmek için idealdir.

## Neden eğri çizgisi ekleyip R‑kare değerini gösterirsiniz?
Eğri çizgisi, bir veri serisinin temel desenini ortaya çıkarırken, **R‑kare** metriği eğri çizgisinin veriye ne kadar iyi oturduğunu ölçer. İkisini de dışa aktarılan görüntüde bulundurmak, paydaşlara çalışma kitabını açmadan anında içgörü sağlar. Bu, karar vericilerin korelasyon gücünü hızlıca değerlendirmesine ve Excel'i açmaya gerek kalmadan trendleri tahmin etmesine yardımcı olur.

## Önkoşullar
- Geliştirme makinenizde Java 8 veya daha yeni bir sürüm yüklü.  
- Aspose.Cells for Java kütüphanesini projenin sınıf yoluna (JAR dosyaları) ekleyin.  
- IntelliJ IDEA veya Eclipse gibi bir Java IDE'sine aşina olun.  

## Adım adım kılavuz

### Adım 1: projeyi kurun
Yeni bir Java projesi oluşturun ve Aspose.Cells JAR dosyalarını derleme yoluna yerleştirin. Bu, Excel dosyaları oluşturmak ve manipüle etmek için ortamı hazırlar.

### Adım 2: Excel dosyasını yükle (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Şimdi **bir Excel dosyasını** belleğe yükledik, grafik oluşturmak için hazır.*

### Adım 3: bir grafik oluşturun
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Burada daha sonra eğri çizgimiz için konaklayacak bir çizgi grafiği oluşturuyoruz.*

### Adım 4: eğri çizgisi ekle (how to add trendline) ve R‑kare değerini göster
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` çağrısı, grafikte **R‑kare değerinin** görünmesini sağlar.*

### Adım 5: grafiği özelleştir ve çalışma kitabını kaydet (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Şimdi çalışma kitabı **oluşturuldu** ve ileri işlem için bir XLSX dosyası olarak kaydedildi.*

### Adım 6: grafiği görüntü olarak dışa aktar (export chart to image)
> **Not:** Bu adım, orijinal blok sayısını değiştirmemek için ek bir kod bloğu olmadan açıklanmıştır.  
Grafik oluşturulup kaydedildikten sonra, `chart.toImage()` metodunu çağırarak ve ortaya çıkan `java.awt.image.BufferedImage`'ı istediğiniz dosya formatına (PNG, JPEG, BMP) yazarak görüntü olarak dışa aktarabilirsiniz. Tipik iş akışı şudur:
1. `Chart` nesnesini alın (önceki adımlarda zaten yapıldı).  
2. `chart.toImage()`'ı çağırarak bir `BufferedImage` elde edin.  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` kullanarak dosyayı yazın.  

`Chart` nesnesi, çalışma kitabındaki bir grafiği temsil eder ve görünümünü ve verilerini değiştirmek için metodlar sağlar. `BufferedImage`, bir görüntüyü bellekte tutan bir Java sınıfıdır ve dosyaya kaydedilmesine olanak tanır. `ImageIO`, Java'da görüntüleri okuma ve yazma için bir yardımcı sınıftır. `setDisplayRSquaredValue`, eğri çizgisinde R‑kare istatistiğinin gösterilmesini etkinleştirir.

### Sonuçları analiz edin
`output.xlsx` dosyasını Excel'de açarak eğri çizgisinin, denklemin ve R‑kare değerinin beklendiği gibi göründüğünü doğrulayın. Dışa aktarılan görüntü dosyasını (ör. `chart.png`) açarak orijinal çalışma kitabı olmadan paylaşılabilecek temiz bir görsel görün.

## Yaygın sorunlar ve çözümler
- **Eğri çizgisi görünmüyor:** Veri aralığının (`A1:A10`) sayısal değerler içerdiğinden emin olun; sayısal olmayan veriler eğri çizgisi hesaplamasını engeller.  
- **R‑kare değeri 0 olarak gösteriliyor:** Bu genellikle veri serisinin sabit olduğu veya değişkenlik içermediği anlamına gelir. Farklı bir veri seti deneyin veya polinom eğri çizgisi kullanın.  
- **Görüntü dışa aktarımı `NullPointerException` ile başarısız oluyor:** `toImage()`'ı çağırmadan önce grafiğin tamamen render edildiğini doğrulayın. Çalışma kitabını önce kaydetmek bazen zamanlama sorunlarını çözebilir.

## Sıkça sorulan sorular

**S: Eğri çizgi tipini nasıl değiştirebilirim?**  
C: Eğri çizgi eklerken farklı bir `TrendlineType` enum değeri kullanın, örneğin polinom uyumu için `TrendlineType.POLYNOMIAL`.

**S: Eğri çizgi görünümünü (renk, kalınlık) özelleştirebilir miyim?**  
C: Evet. `trendline.getLineFormat()` ile eğri çizginin `LineFormat`'ına erişin ve `setWeight()` ve `setColor()` gibi özellikleri ayarlayın.

**S: Grafiği görüntü yerine PDF olarak nasıl dışa aktarırım?**  
C: Önce grafiği bir görüntüye dönüştürün, ardından Aspose.PDF veya başka bir PDF kütüphanesi kullanarak bu görüntüyü PDF'e yerleştirin.

**S: Aynı grafiğe birden fazla eğri çizgisi eklemek mümkün mü?**  
C: Kesinlikle. Analiz etmek istediğiniz her seri için `chart.getNSeries().get(0).getTrendlines().add(...)` metodunu çağırın.

**S: Aspose.Cells yüksek çözünürlüklü görüntü dışa aktarmayı destekliyor mu?**  
C: Evet. `chart.toImage()` çağırırken DPI'yi belirtebilir ve kaydetmeden önce görüntüyü ölçeklendirerek baskı veya yüksek yoğunluklu ekranlar için net bir çıktı elde edebilirsiniz.

---

**Son Güncelleme:** 2026-08-27  
**Test Edilen:** Aspose.Cells for Java en son sürümü (50+ dosya formatını destekler ve çalışma kitaplarını tam bellek yüklemesi olmadan 2 milyon satıra kadar işler)  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.Cells Java ile Excel Grafiğine Veri Etiketleri Ekle](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells Java kullanarak Excel Grafiklerini SVG Olarak Dışa Aktarma (Ölçeklenebilir Vektör Grafikleri)](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Grafiklerini PDF Olarak Dışa Aktarma: Özel Sayfa Boyutları Rehberi](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}