---
date: 2026-02-14
description: Aspose.Cells for Java kullanarak grafiği PNG olarak dışa aktarmayı, veri
  serisi eklemeyi, çizgi‑sütun grafiğini birleştirmeyi, çalışma kitabını XLSX olarak
  kaydetmeyi ve grafik efsanesini eklemeyi öğrenin.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Grafiği PNG olarak dışa aktar ve birleşik grafik için veri serisi ekle
url: /tr/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

 => "Grafiği PNG Olarak Dışa Aktar ve Birleşik Grafik İçin Veri Serileri Ekle". Keep heading.

Also ensure we keep markdown formatting.

Now produce final content with all translations.

We must keep shortcodes at top and bottom unchanged.

Let's construct.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafiği PNG Olarak Dışa Aktar ve Birleşik Grafik İçin Veri Serileri Ekle

Bu öğreticide **veri serileri** ekleyecek, **çizgi ve sütun grafik** öğelerini birleştirecek ve Aspose.Cells for Java kullanarak **grafiği PNG olarak dışa aktar**mayı öğreneceksiniz. Çalışma kitabını ayarlamaktan, grafiği bir çalışma sayfasına eklemeye, lejandı özelleştirmeye, **workbook as xlsx** kaydetmeye ve grafiğin PNG görüntüsünü oluşturmaya kadar her adımı adım adım göstereceğiz. Sonunda, raporlar veya panolar içinde gömebileceğiniz hazır bir birleşik grafik elde edeceksiniz.

## Hızlı Yanıtlar
- **Hangi kütüphane birleşik grafikler oluşturur?** Aspose.Cells for Java  
- **Veri serisi nasıl eklenir?** `chart.getNSeries().add(...)` kullanın  
- **Grafik PNG olarak nasıl dışa aktarılır?** `chart.toImage("file.png", ImageFormat.getPng())` çağırın  
- **Çalışma kitabı hangi dosya formatında kaydedilebilir?** Standart `.xlsx` (workbook as xlsx)  
- **Üretim ortamında lisans gerekli mi?** Geçerli bir Aspose.Cells lisansı gereklidir  

## Aspose.Cells'ta **export chart to PNG** nedir?
Grafiği PNG olarak dışa aktarmak, Excel grafiğinin web sayfalarında, raporlarda veya e‑postalarda Excel uygulamasına ihtiyaç duymadan görüntülenebilen bir raster görüntüsünü oluşturur.

## Neden **combined line column chart** oluşturmalısınız?
Bir birleşik grafik, farklı veri setlerini ayrı görsel temsillerle (ör. bir çizgi serisi bir sütun serisinin üzerine) tek bir görünümde göstermenizi sağlar. Bu, trendleri toplamlarla karşılaştırmak, korelasyonları vurgulamak veya daha kompakt bir formatta zengin içgörüler sunmak için mükemmeldir.

## Önkoşullar
- Java Development Kit (JDK) 8 veya üzeri  
- Aspose.Cells for Java kütüphanesi (aşağıdaki bağlantıdan indirin)  
- Java sözdizimi ve Excel kavramlarına temel aşinalık  

## Başlarken

İlk olarak, resmi siteden Aspose.Cells for Java kütüphanesini indirin:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR dosyasını projenizin sınıf yoluna ekledikten sonra grafiği oluşturmaya başlayabilirsiniz.

### Adım 1: Aspose.Cells sınıflarını içe aktar
```java
import com.aspose.cells.*;
```

### Adım 2: Yeni bir çalışma kitabı oluştur
```java
Workbook workbook = new Workbook();
```

### Adım 3: İlk çalışma sayfasına eriş
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Adım 4: Çalışma sayfasına bir birleşik grafik nesnesi ekle  
İlk olarak bir çizgi grafiği oluşturacağız ve daha sonra bir sütun serisi ekleyerek **combined line column chart** etkisini elde edeceğiz.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Grafiğe Veri Ekleme

Grafik konteyneri oluşturulduğuna göre, ona veri beslememiz gerekiyor.

### Adım 5: Veri aralıklarını tanımla ve **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **İpucu:** İlk parametre (`"A1:A5"`) ilk seri için aralıktır, ikinci parametre (`"B1:B5"`) ise ilk seriyle birleştirilecek ikinci bir seri oluşturur.

### Adım 6: Kategori (X‑ekseni) verisini ayarla
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Grafiği Özelleştirme

İyi bir grafik bir hikâye anlatır. Başlıklar, eksen etiketleri ve net bir lejand ekleyelim.

### Adım 7: **Set chart axis labels** ve başlığı ayarla
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Adım 8: **Add legend chart** ekle ve konumunu ayarla
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Grafiği Kaydetme ve Dışa Aktarma

Özelleştirmeyi tamamladıktan sonra **workbook as xlsx** kaydetmek ve bir görüntü oluşturmak isteyeceksiniz.

### Adım 9: Çalışma kitabını bir Excel dosyası (xlsx) olarak kaydet
```java
workbook.save("CombinedChart.xlsx");
```

### Adım 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` yöntemi **generates excel chart** görüntülerini web sayfalarında, raporlarda veya e‑postalarda kullanılabilecek şekilde üretir.

## Yaygın Sorunlar ve Sorun Giderme

| Sorun | Çözüm |
|-------|----------|
| **Veri görünmüyor** | Hücre aralıklarının (`A1:A5`, `B1:B5`, `C1:C5`) gerçekten veri içerdiğini grafiği oluşturmadan önce doğrulayın. |
| **Lejand grafikle çakışıyor** | `chart.getLegend().setOverlay(false)` ayarlayın veya lejandı farklı bir konuma taşıyın (ör. `RIGHT`). |
| **Görüntü dosyası boş** | Grafiğin en az bir serisi olduğundan ve `chart.toImage` metodunun tüm özelleştirmelerden sonra çağrıldığından emin olun. |
| **Kaydetme sırasında istisna atılıyor** | Hedef dizine yazma izninizin olduğundan ve dosyanın Excel'de açık olmadığından emin olun. |

## Sık Sorulan Sorular

**S: Aspose.Cells for Java nasıl kurulur?**  
C: JAR dosyasını resmi siteden indirin ve projenizin sınıf yoluna ekleyin. İndirme bağlantısı: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**S: Çizgi ve sütun dışında başka grafik türleri oluşturabilir miyim?**  
C: Evet, Aspose.Cells bar, pie, scatter, area ve daha birçok grafik türünü destekler. Tam liste için API belgelerine bakın.

**S: Üretim ortamında lisans gerekli mi?**  
C: Üretim dağıtımları için geçerli bir Aspose.Cells lisansı zorunludur. Değerlendirme için ücretsiz bir deneme sürümü mevcuttur.

**S: Her serinin renklerini nasıl değiştirebilirim?**  
C: Serileri ekledikten sonra `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (veya benzeri) kullanın.

**S: Daha fazla kod örneği nerede bulunur?**  
C: Kapsamlı dokümantasyon ve ek örnekler Aspose referans sitesinde mevcuttur: [here](https://reference.aspose.com/cells/java/).

---

**Son Güncelleme:** 2026-02-14  
**Test Edilen:** Aspose.Cells for Java latest version  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}