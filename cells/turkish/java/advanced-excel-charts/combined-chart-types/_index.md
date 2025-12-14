---
date: 2025-12-06
description: Aspose.Cells for Java ile veri serileri eklemeyi, birleşik grafik türleri
  oluşturmayı, çalışma kitabını Excel olarak kaydetmeyi ve grafiği PNG olarak dışa
  aktarmayı öğrenin.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells kullanarak birleştirilmiş grafik oluşturmak için veri serileri
  ekleyin
url: /tr/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells kullanarak birleşik grafik oluşturmak için veri serisi ekleme

Bu öğreticide **veri serisi ekleyecek** ve Aspose.Cells for Java ile **birleşik grafik** türleri oluşturmayı öğreneceksiniz. Çalışma kitabını ayarlamaktan, serileri eklemeye, lejandı özelleştirmeye, **Excel çalışma kitabını kaydetmeye** ve **grafiği PNG olarak dışa aktarmaya** kadar her adımı adım adım göstereceğiz. Sonunda, raporlar veya panolar içinde gömebileceğiniz kullanıma hazır bir birleşik grafiğe sahip olacaksınız.

## Quick Answers
- **Birleşik grafikleri hangi kütüphane oluşturur?** Aspose.Cells for Java  
- **Bir veri serisi nasıl eklenir?** Use `chart.getNSeries().add(...)`  
- **Grafiği görüntü olarak dışa aktarabilir miyim?** Yes, with `chart.toImage(...)` (PNG)  
- **Çalışma kitabını hangi dosya formatında kaydedebilirim?** Standard `.xlsx` (Excel)  
- **Üretim için lisansa ihtiyacım var mı?** A valid Aspose.Cells license is required  

## Aspose.Cells'ta **veri serisi ekleme** nedir?
Bir veri serisi eklemek, grafiğe hangi hücrelerin çizmek istediğiniz değerleri içerdiğini söyler. Her seri bir çizgi, sütun veya başka bir grafik türünü temsil edebilir ve bunları karıştırarak bir **birleşik grafik** oluşturabilirsiniz.

## Neden **birleşik grafik** oluşturmalısınız?
Bir birleşik grafik, farklı veri setlerini ayrı görsel temsillerle (ör. bir sütun serisi üzerine bir çizgi serisi) tek bir görünümde göstermenizi sağlar. Bu, trendleri toplamlarla karşılaştırmak, korelasyonları vurgulamak veya daha kompakt bir formatta zengin içgörüler sunmak için mükemmeldir.

## Önkoşullar
- Java Development Kit (JDK) 8 veya üzeri  
- Aspose.Cells for Java kütüphanesi (aşağıdaki bağlantıdan indirin)  
- Java sözdizimi ve Excel kavramları hakkında temel bilgi  

## Başlarken

İlk olarak, resmi siteden Aspose.Cells for Java kütüphanesini indirin:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR dosyası projenizin sınıf yoluna eklendikten sonra grafiği oluşturmaya başlayabilirsiniz.

### Adım 1: Aspose.Cells sınıflarını içe aktarın
```java
import com.aspose.cells.*;
```

### Adım 2: Yeni bir çalışma kitabı oluşturun
```java
Workbook workbook = new Workbook();
```

### Adım 3: İlk çalışma sayfasına erişin
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Adım 4: Bir birleşik grafik nesnesi ekleyin  
İlk olarak bir çizgi grafiği oluşturacağız ve daha sonra diğer serileri ekleyerek **birleşik grafik** etkisini elde edeceğiz.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Grafiğe Veri Ekleme

Grafik konteyneri oluşturulduğuna göre, ona veri beslememiz gerekiyor.

### Adım 5: Veri aralıklarını tanımlayın ve **veri serisi ekleyin**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro ipucu:** İlk parametre (`"A1:A5"`) ilk serinin aralığıdır ve ikinci parametre (`"B1:B5"`) ilk seriyle birleştirilecek ikinci bir seri oluşturur.

### Adım 6: Kategori (X‑ekseni) verisini ayarlayın
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Grafiği Özelleştirme

İyi bir grafik bir hikaye anlatır. Ona başlıklar, eksen etiketleri ve net bir lejand verelim.

### Adım 7: Grafik başlığını ve eksen etiketlerini ayarlayın
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Adım 8: **Lejand grafiği ekleyin** ve konumunu ayarlayın
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Grafiği Kaydetme ve Dışa Aktarma

Özelleştirmeden sonra **Excel çalışma kitabını kaydetmek** ve ayrıca bir görüntü oluşturmak isteyeceksiniz.

### Adım 9: Çalışma kitabını Excel dosyası olarak kaydedin
```java
workbook.save("CombinedChart.xlsx");
```

### Adım 10: **Grafiği PNG olarak dışa aktarın**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` yöntemi **Excel grafiği** görüntüleri oluşturur ve bu görüntüler web sayfalarında, raporlarda veya e-postalarda kullanılabilir.

## Yaygın Sorunlar ve Sorun Giderme

| Sorun | Çözüm |
|-------|----------|
| **Veri görünmüyor** | Grafik oluşturulmadan önce hücre aralıklarının (`A1:A5`, `B1:B5`, `C1:C5`) gerçekten veri içerdiğini doğrulayın. |
| **Lejand grafikle çakışıyor** | `chart.getLegend().setOverlay(false)` ayarlayın veya lejandı farklı bir konuma taşıyın (ör. `RIGHT`). |
| **Görüntü dosyası boş** | Grafiğin en az bir serisi olduğundan ve `chart.toImage` yönteminin tüm özelleştirmelerden sonra çağrıldığından emin olun. |
| **Kaydetme bir istisna fırlatıyor** | Hedef dizine yazma izniniz olduğundan ve dosyanın Excel'de açık olmadığından emin olun. |

## Sık Sorulan Sorular

**S: Aspose.Cells for Java nasıl kurulur?**  
C: JAR dosyasını resmi siteden indirip projenizin sınıf yoluna ekleyin. İndirme bağlantısı: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**S: Çizgi ve sütun dışında başka grafik türleri oluşturabilir miyim?**  
C: Evet, Aspose.Cells çubuk, pasta, dağılım, alan ve daha birçok grafik türünü destekler. Tam liste için API belgelerine bakın.

**S: Üretim kullanımında lisans gerekli mi?**  
C: Üretim dağıtımları için geçerli bir Aspose.Cells lisansı gereklidir. Değerlendirme için ücretsiz deneme mevcuttur.

**S: Her serinin renklerini nasıl değiştirebilirim?**  
C: Serileri ekledikten sonra `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (veya benzeri) yöntemini kullanın.

**S: Daha fazla kod örneği nerede bulunabilir?**  
C: Kapsamlı dokümantasyon ve ek örnekler Aspose referans sitesinde bulunabilir: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
