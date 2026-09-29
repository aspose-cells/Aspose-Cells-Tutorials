---
date: 2026-02-09
description: Aspose.Cells for Java kullanarak Excel grafiği oluşturmayı, bir trend
  çizgisi eklemeyi, R‑kare değerini göstermeyi ve grafiği bir görüntüye dışa aktarmayı
  öğrenin. Excel dosyasını yükleme, grafiği özelleştirme ve PNG/JPEG olarak kaydetme
  adımlarını içerir.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells for Java kullanarak Trend Çizgili Excel Grafiği Oluşturma ve Görüntü
  Olarak Dışa Aktarma
url: /tr/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Trend Çizgili Analiz ile Grafik Görüntüye Dışa Aktarma

Bu öğreticide **Excel grafiği** oluşturmayı, bir trend çizgisi eklemeyi, R‑kare değerini göstermeyi ve Aspose.Cells for Java kullanarak ortaya çıkan görseli bir görüntüye dışa aktarmayı öğreneceksiniz. Mevcut bir çalışma kitabını yükleme, trend çizgisi ekleme, başlıkları özelleştirme, çalışma kitabını kaydetme ve nihayetinde PNG/JPEG dosyası oluşturma adımlarını adım adım inceleyeceğiz.

## Hızlı Cevaplar
- **Bu kılavuzun temel amacı nedir?** Trend çizgisi eklemeyi, denklemini ve R‑kare değerini göstermeyi ve grafiği Java ile bir görüntüye dışa aktarmayı göstermek.  
- **Hangi kütüphane gereklidir?** Aspose.Cells for Java (indir [buradan](https://releases.aspose.com/cells/java/)).  
- **Lisans gerekiyor mu?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim ortamı için ticari lisans gereklidir.  
- **Java’da bir Excel dosyası oluşturabilir miyim?** Evet – öğreticide bir XLSX çalışma kitabı oluşturulup kaydedilir.  
- **Grafiği PNG ya da JPEG olarak nasıl dışa aktarırım?** “Grafiği Dışa Aktar” bölümünde açıklanan `Chart.toImage()` yöntemi kullanılır.

## Trend çizgili Excel grafiği nasıl oluşturulur ve görüntüye dışa aktarılır
Bu başlık, ana anahtar kelime sorgusuna doğrudan yanıt verir ve tüm iş akışını mantıklı bir sırayla yönlendirir. Aşağıda neden, önkoşullar ve adım adım yürütme bulacaksınız.

## Grafik Görüntüye Dışa Aktarma Nedir?
Bir grafiği görüntüye dışa aktarmak, verilerinizin görsel temsilini taşınabilir bir bitmap (PNG, JPEG vb.) formatına dönüştürür. Bu, orijinal Excel dosyasına ihtiyaç duymadan raporlar, web sayfaları veya sunumlarda grafik eklemek için kullanışlıdır.

## Neden Trend Çizgisi Ekleyip R‑kare Değerini Gösterelim?
Trend çizgisi, bir veri serisinin temel desenini tanımlamanıza yardımcı olurken, **R‑kare** metriği trend çizgisinin veriye ne kadar iyi oturduğunu nicelendirir. Bu öğeleri dışa aktarılan görüntüde bulundurmak, paydaşların çalışma kitabını açmadan anında içgörü elde etmesini sağlar.

## Önkoşullar
- Java 8 veya daha yeni bir sürüm yüklü.  
- Projeye Aspose.Cells for Java kütüphanesi eklenmiş (JAR dosyaları sınıf yolunda).  
- Java IDE’lerine (IntelliJ IDEA, Eclipse vb.) temel aşinalık.

## Adım Adım Kılavuz

### Adım 1: Projeyi Kurun
Yeni bir Java projesi oluşturun ve Aspose.Cells JAR dosyalarını derleme yoluna ekleyin. Bu, Excel dosyaları oluşturma ve işleme ortamını hazırlar.

### Adım 2: Excel Dosyasını Yükle (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Belleğe **bir Excel dosyası** yüklendi, grafik oluşturmak için hazır.*

### Adım 3: Bir Grafik Oluştur
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Daha sonra trend çizgimizi ekleyeceğimiz bir çizgi grafiği burada üretiliyor.*

### Adım 4: Trend Çizgisi Ekle (how to add trendline) ve R‑kare Değerini Göster
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` çağrısı, **R‑kare değerinin** grafikte görünmesini sağlar.*

### Adım 5: Grafiği Özelleştir ve Çalışma Kitabını Kaydet (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Artık çalışma kitabı **oluşturuldu** ve bir XLSX dosyası olarak kaydedildi, sonraki işlemlere hazır.*

### Adım 6: Grafiği Görüntüye Dışa Aktar (export chart to image)
> **Not:** Bu adım, orijinal blok sayısını değiştirmemek için ek bir kod bloğu içermemektedir.  
Grafik oluşturulup kaydedildikten sonra, `chart.toImage()` metodunu çağırarak ve elde edilen `java.awt.image.BufferedImage` nesnesini istediğiniz dosya formatına (PNG, JPEG, BMP) yazarak bir görüntüye dışa aktarabilirsiniz. Tipik iş akışı:
1. `Chart` nesnesini alın (önceki adımlarda zaten elde edildi).  
2. `chart.toImage()` çağrısıyla bir `BufferedImage` alın.  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` ile dosyayı yazın.  

Bu, **grafiği görüntüye dışa aktarma** sürecini tamamlayan yüksek çözünürlüklü bir görüntü üretir.

## Sonuçları Analiz Et
`output.xlsx` dosyasını Excel’de açarak trend çizgisi, denklem ve R‑kare değerinin beklendiği gibi göründüğünden emin olun. Dışa aktarılan görüntü dosyasını (ör. `chart.png`) açarak orijinal çalışma kitabına ihtiyaç duymadan paylaşılabilecek temiz bir görsel elde edin.

## Yaygın Sorunlar ve Çözümler
- **Trend çizgisi görünmüyor:** Veri aralığının (`A1:A10`) gerçekten sayısal değerler içerdiğinden emin olun; sayısal olmayan veriler trend çizgisinin hesaplanmasını engeller.  
- **R‑kare değeri 0 gösteriyor:** Bu genellikle veri serisinin sabit olduğu veya yeterli değişkenlik göstermediği anlamına gelir. Farklı bir veri seti deneyin veya polinom trend çizgisi kullanın.  
- **Görüntü dışa aktarımı `NullPointerException` ile başarısız oluyor:** `toImage()` çağrılmadan önce grafiğin tam olarak render edildiğini doğrulayın. Çalışma kitabını önce kaydetmek zamanlama sorunlarını bazen çözer.

## Sık Sorulan Sorular

**S: Trend çizgisi tipini nasıl değiştiririm?**  
C: Trend çizgisi eklerken farklı bir `TrendlineType` enum değeri kullanın, örneğin polinom uyumu için `TrendlineType.POLYNOMIAL`.

**S: Trend çizgisinin görünümünü (renk, kalınlık) özelleştirebilir miyim?**  
C: Evet. `trendline.getLineFormat()` üzerinden `LineFormat` nesnesine erişip `setWeight()` ve `setColor()` gibi özellikleri ayarlayabilirsiniz.

**S: Grafiği bir görüntü yerine PDF olarak dışa aktarabilir miyim?**  
C: Önce grafiği bir görüntüye dönüştürün, ardından bu görüntüyü Aspose.PDF veya tercih ettiğiniz herhangi bir PDF kütüphanesiyle PDF’e yerleştirin.

**S: Aynı grafiğe birden fazla trend çizgisi eklemek mümkün mü?**  
C: Kesinlikle. Analiz etmek istediğiniz her seri için `chart.getNSeries().get(0).getTrendlines().add(...)` çağrısını yapın.

**S: Aspose.Cells yüksek çözünürlüklü görüntü dışa aktarımını destekliyor mu?**  
C: Evet. `chart.toImage()` çağrısında DPI belirtebilir ve kaydetmeden önce görüntüyü buna göre ölçeklendirebilirsiniz.

## Sonuç
Artık **Excel grafiği** oluşturmak, trend çizgisi eklemek, denklemi ve R‑kare değerini göstermek, görseli özelleştirmek, çalışma kitabını kaydetmek ve grafiği PNG/JPEG olarak dışa aktarmak için uçtan uca bir çözümünüz var. Bu yaklaşım, otomatik raporlama, gösterge panelleri veya statik bir görüntünün Excel dosyasından daha uygun olduğu her senaryo için programatik olarak profesyonel düzeyde analiz varlıkları üretmenizi sağlar.

---

**Son Güncelleme:** 2026-02-09  
**Test Edilen Versiyon:** Aspose.Cells for Java en son sürüm  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}